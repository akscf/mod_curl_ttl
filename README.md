<p>
  TTS module that allows to work with text-to-speech tools over http. <br>
  The backend should be able to process POST requests with json payload: { "language": "en", "text" : "Some text to tts" , [speak extra args may follow here] } <br>
  The response should be one of the types: audio/mpeg for mp3 and audio/wav for wav respectively.
</p>

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
