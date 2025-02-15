<p>
  This module allows to work with text-to-speech tools over http. <br>
  Designed to work in tandem with <a href="https://github.com/akscf/ttsd">ttsd</a>
</p>

### Few words about backend
<p>
    The payload encoded with JSON and carries over POST method, with the following format: { "language": "en", "text": "Some text to tts"} <br>
    There are two mandatory attribures, language and text, the tts custom parameters will be attached after ones. <br>
    The response should be one of the types: <br>
    <ul>
	<li><strong>MP3</strong> content-type: audio/mp3</li>
	<li><strong>WAV</strong> content-type: audio/wav</li>
    </ul>
</p>

### Build and installation
 if you already have installed freeswitch and its sources: 
 - Unpack the module sources into 'src/mod/asr_tts/mod_curl_tts'
 - go to freeswitch root and edit 'configure.ac', look for variable 'AC_CONFIG_FILES' and add this module (src/mod/asr_tts/mod_curl_tts/Makefile) after 'mod_abstraction' 
 - perform: make clean (you should see how libtool rebuilding Makefiles, if it doesn't, you did something wrong) 
 - after that goto 'src/mod/asr_tts/mod_curl_tts' and perform: make clean all install 
   and copy configuration 'conf/autoload_configs/curl_tts.conf.xml' to freeswitch configs dir manually.

### Usage example
```XML
<extension name="tts-test1">
    <condition field="destination_number" expression="^(3333)$">
        <action application="answer"/>
        <action application="speak" data="curl|en|Hello world!"/>
        <action application="sleep" data="1000"/>
        <action application="hangup"/>
    </condition>
</extension>

<extension name="tts-test2">
    <condition field="destination_number" expression="^(3334)$">
        <action application="answer"/>
	<action application="speak" data="curl|en|{arg1=val1,arg2=val2,url=http://127.0.0.1:8080/tts}Hello, test 123"/>
        <action application="sleep" data="1000"/>
        <action application="hangup"/>
    </condition>
</extension>

```
