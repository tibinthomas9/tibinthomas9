---
layout: post
title: iOS Rich Notifications and how to play a youtube video within a notification
subtitle: ios
comments: true
---
<hr>
<p><img src="https://cdn-images-1.medium.com/max/2560/1*tbPq5hncRE-kYaXxgFs60g.png" alt=""></p>
<p>from  <a href="https://www.apple.com/">apple</a></p>
<p>In iterative iOS releases apple incorporated new features into the iOS notification system.The aim of the new features was to provide a more  <strong>immersive and interactive experience for the user within the notification</strong>.Thus users would be able to get more information and also perform critical action right within the notification without the need of opening the app.</p>
<p>The most prominent features among them are:</p>
<ol>
<li><strong>Notification Actions</strong>: provides the actions that the user can perform to interact with the notification message. They are presented as buttons. Available via  <a href="http://www.thinkandbuild.it/interactive-notifications-with-notification-actions/"><strong>UIUserNotificationAction</strong></a><strong>.</strong></li>
<li><strong>Text Input in Notification Actions:</strong> Provides the user the ability to input text within a notification.Implemented via  <a href="https://developer.apple.com/documentation/usernotifications/untextinputnotificationaction">UNTextInputNotificationAction</a>.</li>
<li><strong>Grouped Notifications</strong>: Ability to group similar notification into a single group so that the notification center remains clean and also to provide more control and information to the user.iOS automatically groups notifications or you can implement your custom grouping via  <a href="https://medium.com/swift-india/lets-take-quick-dive-in-grouped-notifications-5d41af9d6463"><strong>threadIdentifier</strong></a>.</li>
<li><strong>Silent Notifications:</strong> Can be used to update contents in the app silently in the background.These type of notifications does not display an alert, play a sound, or badge your app’s icon.Implemented via  <a href="https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/pushing_updates_to_your_app_silently">content-available</a> key.</li>
<li><strong>Notification Attachments</strong>: Attach audio, image, or video content together in an alert-based notification.Implemented via  <a href="https://developer.apple.com/documentation/usernotifications/unnotificationattachment"><strong>UNNotificationAttachment</strong></a>  and  <a href="https://developer.apple.com/documentation/usernotifications/unnotificationserviceextension"><strong>UNNotificationServiceExtension</strong></a><strong>.</strong></li>
<li><strong>Custom Notification UI:</strong>  Customise the UI of the notification.Implemented via  <a href="https://developer.apple.com/documentation/usernotificationsui/unnotificationcontentextension"><strong>UNNotificationContentExtension</strong></a><strong>.</strong></li>
<li><strong>Interactive Controls</strong>  <strong>in Custom UI</strong>: Ability to add custom controls within the UI so that users can  <a href="https://developer.apple.com/documentation/usernotificationsui/customizing_the_appearance_of_notifications">interact</a>  within the notifications.</li>
</ol>
<h3 id="playing-youtube-video-within-a-notification">Playing Youtube Video within a Notification</h3>
<p>Among the capabilities of push notification in iOS ,you can add custom UI<br>
to a notification wherein you can provide custom content including text,audio,video and gifs.These features are implemented using  <a href="https://developer.apple.com/documentation/usernotifications/unnotificationserviceextension">UNNotificationServiceExtension</a>  and  <a href="https://developer.apple.com/documentation/usernotificationsui/unnotificationcontentextension">UNNotificationContentExtension</a>  as noted <a href="http://above.To">above.To</a> play a video you can either download the video and provide it as a  <a href="https://developer.apple.com/documentation/usernotifications/unnotificationattachment">UNNotificationAttachment</a>  or you can play a web link using  <a href="https://developer.apple.com/documentation/avfoundation/avplayer">AVPlayer</a>. But you can’t play a youtube video using these methods .Here I am going to explain how I enabled playing youtube videos within a notification.</p>
<p>To enable playing youtube videos within an iOS aspplication,google provides a library called  <a href="https://developers.google.com/youtube/v3/guides/ios_youtube_helper"><strong>youtube-ios-player-helper</strong></a><strong>,</strong> which helps you embed a YouTube iframe player into an iOS application. The library creates a  <a href="https://developer.apple.com/library/ios/documentation/uikit/reference/UIWebView_Class/Reference/Reference.html">UIWevView</a>  and a bridge between your application’s code and the YouTube player’s JavaScript code, thereby allowing the iOS application to control the YouTube player.</p>
<p>Here we combine the  <a href="https://developer.apple.com/documentation/usernotificationsui/unnotificationcontentextension"><em>UNNotificationContentExtension</em></a><strong>(<strong>which is used to create custom UI for notification</strong>)</strong> and  <em>youtube-ios-player-helper</em>  to enable playingyoutube videos within a notification.</p>
<p>So first we need to  <a href="https://developer.apple.com/documentation/usernotificationsui/customizing_the_appearance_of_notifications?language=objc">add a notification</a>  content app extension to the project.Then you specify the  <em>category</em>  for the particular extension in its Info.plist.This category names is used to determine whether the content extension is to be used when a notification arrives.</p>
<p>The created extension consists of a  <em>Storyboard</em>  file(which contains the view controller to be used as our custom UI) and a  <em>ViewController</em>  class which conforms to  <em>UNNotificationContentExtension</em>  protocol.You can configure the custom UI when the notification arrives using the  <code>didReceive(_ notification: UNNotification)</code>  method.</p>
<p>To support playing youtube video we need to</p>
<ol>
<li>
<p>Install youtube-ios-player-helper as a  <em>pod</em></p>
</li>
<li>
<p><em>Import</em>  youtube_ios_player_helper in our extensions viewcontroller class.</p>
</li>
<li>
<p>Add a view to our viewcontroller in storyboard and set its class as YTPlayerView and then add an outlet(this view enables playing youtube video)</p>
</li>
<li>
<p>Then in the didReceiveNotification method we extract the video url from the notification payload(which needs to be added as a custom parameter).</p>
<pre><code>func didReceive(_ notification: UNNotification) {

if let attachmentURL = notification.request.content.userInfo["video-url"] as? String, let url
= URL(string: attachmentURL){

ytPlayerView.isHidden = false

ytPlayerView.delegate = self

if let linkID = extractYoutubeIdFromLink(link: attachmentURL){

let playerVars = [ "playsinline" : 1]

self.ytPlayerView.load(withVideoId: linkID, playerVars: playerVars)

   }  
  }  
}
</code></pre>
</li>
<li>
<p>Then extract the youtubeId from the url using regEx.</p>
<pre><code> func extractYoutubeIdFromLink(link: String) -&gt; String? {
 
 let pattern = "((?&lt;=(v|V)/)|(?&lt;=be/)|(?&lt;=(\\?|\\&amp;)v=)|(?&lt;=embed/))([\\w-]++)"
 guard let regExp = try? NSRegularExpression(pattern: pattern, options: .caseInsensitive) else {

 return nil   }

 let nsLink = link as NSString

 let options = NSRegularExpression.MatchingOptions(rawValue: 0)

 let range = NSRange(location: 0, length: nsLink.length)

 let matches = regExp.matches(in: link as String, options:options, range:range)

 if let firstMatch = matches.first {   return nsLink.substring(with: firstMatch.range)   }   return nil   }
</code></pre>
</li>
<li>
<p>Load the video using ytPlayerView’s loadVideoWithId method and set ytPlayerView outlets delegate to self.</p>
</li>
</ol>
<p>self.ytPlayerView.load(withVideoId: linkID, playerVars: playerVars)</p>
<ol start="7">
<li>When the ytPlayerView becomes ready to play the loaded video it informs us through the delegate method  <em>playerViewDidBecomeReady</em>(<strong>_</strong>  playerView: YTPlayerView_)._In the delegate method we start playing the video</li>
</ol>
<blockquote>
<pre><code> func playerViewDidBecomeReady(**_** playerView: YTPlayerView) {  
           	playerView.playVideo()  
       }
</code></pre>
</blockquote>
<p>Now when the notification arrives and the user selects the notification by dragging the didReceive method is called and the youtube video starts to play.<br>
And we are done.Hip Hip Hooray!.</p>
<ul>
<li>
<p><a href="https://medium.com/tag/ios?source=post">iOS</a></p>
</li>
<li>
<p><a href="https://medium.com/tag/push-notification?source=post">Push Notification</a></p>
</li>
<li>
<p><a href="https://medium.com/tag/custom-ui?source=post">Custom Ui</a></p>
</li>
<li>
<p><a href="https://medium.com/tag/apple?source=post">Apple</a></p>
</li>
<li>
<p><a href="https://medium.com/tag/rich-notification?source=post">Rich Notification</a></p>
</li>
<li>
<p><a href="https://medium.com/@tibinmutholy?source=footer_card" title="Go to the profile of Tibin Thomas"><img src="https://cdn-images-1.medium.com/fit/c/60/60/1*iCzkSKlEB0uod0UoJnkBbQ.jpeg" alt="Go to the profile of Tibin Thomas"></a></p>
<h3 id="tibin-thomas"><a href="https://medium.com/@tibinmutholy" title="Go to the profile of Tibin Thomas">Tibin Thomas</a></h3>
<p>iOS|Open Source|Science &amp; Technology</p>
</li>
</ul>

