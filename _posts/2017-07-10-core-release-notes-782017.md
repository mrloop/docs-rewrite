---
ID: 30459
post_title: 'Mycroft Core Release Notes: 7/8/2017'
author: Steve Penrod
post_excerpt: ""
layout: post
permalink: >
  https://mycroft.ai/blog/core-release-notes-782017/
published: true
post_date: 2017-07-10 10:15:21
---
[vc_row type="in_container" full_screen_row_position="middle" scene_position="center" text_color="dark" text_align="left" overlay_strength="0.3"][vc_column column_padding="no-extra-padding" column_padding_position="all" background_color_opacity="1" background_hover_color_opacity="1" column_shadow="none" width="1/1" tablet_text_alignment="default" phone_text_alignment="default" column_border_width="none" column_border_style="solid"][vc_column_text]
<h2>What's in these release notes?</h2>
We are well into the Mark 1 production run now and have been putting out releases largely focused on that experience. We've also expanded the core capabilities in the process.  Below are the notes for the last several releases.
<h2>mycroft-core 0.8.18</h2>
<h4>Fixes</h4>
<ul>
 	<li>ISSUE #874: Handling $WORKON_HOME in start.sh. Thanks nealmcb! (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/875">875</a>)</li>
 	<li>Mycroft wasn't recognizing the "wake up" phrase to come out of deep sleep mode entered by saying "Hey Mycroft, go to sleep". (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/888">888</a>)</li>
 	<li>ISSUE #871: Automatic skill update was not occurring. Files automatically generated by Python were making the system think the skill was being worked on by a developer. Now the Mycroft Skill Manager (MSM) behavior properly updates skills that have not been modified, but stops updates if a developer intentionally makes changes to the code for a skill. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/873">873</a>, #<a href="https://github.com/MycroftAI/mycroft-core/pull/890">890</a>, #<a href="https://github.com/MycroftAI/mycroft-core/pull/894">894</a>)</li>
</ul>
<h4>Developer and API enhancements</h4>
<ul>
 	<li>Blacklisted skills are now read from a list in the config. The value is under skills.blacklisted_skills. Thanks JarbasAI! (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/857">857</a>)</li>
 	<li>Added support for "mycroft.sh restart" to mycroft.sh utility. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/868">868</a>)</li>
 	<li>Documented the Message class. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/869">869 </a>and #<a href="https://github.com/MycroftAI/mycroft-core/pull/748">748</a>)</li>
 	<li>Intents now can be defined via a "decorator". This replaces the need to create an initialize() method purely for connecting the skill handlers. Here is an example:Decorator-style intent definition</li>
</ul>
<pre style="padding-left: 30px;">   @intent_handler(IntentBuilder('HelloWorldIntent').require('hello').build())
   def handle_hello_world(self, message):
       self.speak('hello!')</pre>
<p style="padding-left: 30px;">Old-style intent definition</p>

<pre style="padding-left: 30px;">   def initialize(self):
       hello_intent = IntentBuilder("HelloWorldIntent").require("hello").build()
       self.register_intent(hello_world_intent, self.handle_hello_world)

   def handle_hello_world(self, message):
       self.speak('hello!')</pre>
<p style="padding-left: 30px;">The old style is still supported and will remain available. But both methods are functionally identical and we believe the new method is simpler and clearer. (PR #865)</p>

<ul>
 	<li>Modularization of Wake Word (similar to TTS and STT). This will allow alternatives to PocketSphinx for wake word spotting. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/876">876</a>)</li>
 	<li>Text to Speech is now unified in an independent thread. This groups multiple-sentence replies and improves handling of for the "Stop" action and button on a Mark 1. This architectural change will also allow things like applying the audio caching mechanism for TTS engines besides the default Mimic, and viseme (mouth shape) support for other TTS providers. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/804">804</a>, #<a href="https://github.com/MycroftAI/mycroft-core/pull/892">892</a>)</li>
 	<li>Removed unused / unneeded libraries from the requirements.txt (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/806">806</a>)</li>
 	<li>Added dev_setup.sh support for using packaged mimic (eliminating the lengthy compile time). Thanks el-tocino and Blackbaud-RyanSnedegar! (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/882">882</a>)</li>
 	<li>Errors encountered during skill update were failing with no indication of why in the logs. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/879">879</a>)</li>
 	<li>Deprecated version mechanism was still being used in setup tools. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/829">829</a>)</li>
</ul>
<h2>mycroft-core 0.8.17</h2>
<h4>Fixes</h4>
<ul>
 	<li>PID and locking mechanism was causing issues on auto-reloads. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/837">837</a>)</li>
</ul>
<h4>Mark 1</h4>
<ul>
 	<li>Added support for menu item SSH &gt; DISABLE and switch to using 'systemctl'. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/744">744</a>, #<a href="https://github.com/MycroftAI/mycroft-core/pull/745">745</a>)</li>
 	<li>Tweaks to wifi-setup disconnect detection (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/861">861</a>)</li>
</ul>
<h4>General</h4>
<ul>
 	<li>Added a docker setup script (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/775">775</a>)</li>
 	<li>Improved multi-core support in dev_setup.sh script (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/823">823</a>)</li>
 	<li>Refinement of mycroft.sh operation (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/835">835</a>)</li>
 	<li>CLI client refinements to support backspace on some terminals and suppress TTS output that occasionally corrupted the screen. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/833">833</a>)</li>
 	<li>Some JSON loads didn't use load_commented_json(), causing issues if devs commented some config files. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/845">845</a>)</li>
 	<li>Added local caching for remote Mycroft config (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/828">828</a>)</li>
 	<li>SkillSettings could miss updates to lists or dicts (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/844">844</a>)</li>
 	<li>Added remove_all_listeners() to EventEmitter on the websocket (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/854">854</a>)</li>
 	<li>MSM enhancements. Added support for Picroft installs, installing list of skills, etc.  Thanks el-tocino! (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/813">813</a>)</li>
</ul>
<h2>mycroft-core 0.8.16 june 13</h2>
<h4>Fixes</h4>
<ul>
 	<li>Issue #807: MSM could report successful install even after a failure. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/813">813</a>)</li>
 	<li>Minor onboarding refinements: no timeout for wifi setup, preventing from talking over itself in certain situations. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/817">817</a>)</li>
 	<li>Rework of has_been_paired() to deal with a changing identity file. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/825">825</a>)</li>
</ul>
<h2>mycroft-core 0.8.15</h2>
<h4>Mark 1</h4>
<ul>
 	<li>Created an 'out of box' experience. This walks a new Mark 1 user through the process of setting up seamlessly and provides a simple introduction to using the device. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/808">808</a>, #<a href="https://github.com/MycroftAI/mycroft-core/pull/811">811</a>)</li>
</ul>
<h4>Enhancements</h4>
<ul>
 	<li>Added mycroft.util.parse.extract_number(). This will support parsing a number out of phrases like "a cup and a half of milk" or "one and three fourths cup", extracting 1.5 and 1.75 respectively.  Thanks ProsperousHeart! (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/793">793</a>)</li>
 	<li>Added mycroft.util.format.nice_number(). This converts numbers into natural spoken phrases, e.g. 3.5 into "three and a half."   Thanks ashwinjv!  (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/786">786</a>)</li>
</ul>
<h4>Fixes</h4>
<ul>
 	<li>Catching of KeyboardInterrupt by a signal handler was causing issues when shutting down services as a developer. Ctrl+C didn't work properly anymore. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/798">798</a>)</li>
 	<li>Scaled the duration of wake-up-word listening based on number of phonemes. This allows longer wake-up phrases to work properly. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/794">794</a>)</li>
 	<li>Fixed broken link in CONTRIBUTING.md (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/784">784</a>)</li>
 	<li>Added check of exit status after calling the Mycroft Skills Manager (MSM) to verify skill install success. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/782">782</a>)</li>
</ul>
<h2>mycroft-core 0.8.14</h2>
<ul>
 	<li>Changed the wifi-setup client password to '12345678' to make easier to type, based on user testing feedback. (PR <a class="issue-link js-issue-link" title="Feature/issue 779 -- Change wifi setup password to &quot;12345678&quot;" href="https://github.com/MycroftAI/mycroft-core/pull/780" data-id="230482140" data-error-text="Failed to load issue title" data-permission-text="Issue title is private">#780</a>)</li>
</ul>
<h2>mycroft-core 0.8.13</h2>
<h4> Fixes</h4>
<ul>
 	<li>Issue #746 : Google STT was broken by a typo (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/750">750</a>)</li>
 	<li>Issue #705: Unable to talk to the API over SSL on some Linux distros. Switching to pyOpenSSL version 16.2.0, resolved it. Thanks BoBeR182! (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/751">751</a>)</li>
</ul>
<h4>Startup sequence</h4>
<ul>
 	<li>Prevented double-announcements when connecting to (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/766">766</a>)</li>
 	<li>Corrected announcement when SSH is enabled/disabled -- reboot is not required anymore. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/765">765</a>)</li>
 	<li>Reworked startup sequence of events and documented behavior. This corrected occasionally not prompting user to connect to the internet and unified the startup prompt and prompts needed if internet is lost later. (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/764">764</a>, <a href="https://github.com/MycroftAI/mycroft-core/pull/760">760</a>)</li>
 	<li>Simplified the package manifest files by adding wildcards to handle resource files under 'mycroft/res/' (PR #<a href="https://github.com/MycroftAI/mycroft-core/pull/763">763</a>)</li>
</ul>
[/vc_column_text][/vc_column][/vc_row]