# 語音轉文字Google API

- 需要一個google帳號，然後用它開啟專案＋計費功能＋開啟API
- 使用 [Google Speech-to-Text](https://cloud.google.com/speech-to-text/docs/quickstart-protocol?_ga=2.81698899.-550699773.1583810055&_gac=1.152614091.1583810055.Cj0KCQjw0pfzBRCOARIsANi0g0u4I9ryqUY60nS5tjGa9ceeLNpDZeonoP1F2nERMX_tLFGE-I0DwOoaAihHEALw_wcB)，按照上面的步驟
    - 選擇Google專案
    - 開啟Google speech to text API
    - 下載key的JSON檔案

    npm install --save @google-cloud/speech

## NodeJS程式範例

- 完整範例

        // Imports the Google Cloud client library
        const speech = require('@google-cloud/speech');
        const fs = require('fs');
        
        // Your Google Cloud Platform project ID
        const projectId = 'mmh-voice-to-text';
        
        // Creates a client
        const client = new speech.SpeechClient({
          projectId: projectId,
          keyFilename: 'credentials/mmh-voice-to-text.json',
        });
        
        
        const voiceToText = (filePath)=> {
          return new Promise((resolove,reject)=>{
            const file = fs.readFileSync(filePath);
            const audioBytes = file.toString('base64');
          
            const audio = {
              content: audioBytes,
            };
          
            const config = {
              encoding: 'ALAC',
              sampleRateHertz: 16000,
              languageCode: 'zh-Hant',
            };
            
            const request = {
              audio: audio,
              config: config,
            };
          
            client
            .recognize(request)
            .then(data => {
              const response = data[0];
              const transcription = response.results
                .map(result => result.alternatives[0].transcript)
                .join('\n');
              console.log('翻譯',transcription)
              return resolove(transcription)
            })
            .catch(err => {
              return reject(err.details)
            });  
          })
        
        }
        
        module.exports = voiceToText

- API驗證設定
    - 啟動google API的時候下載JSON檔案
    - 把credentials的JSON路徑寫在以下設定中

        const client = new speech.SpeechClient({
          projectId: projectId,
          keyFilename: 'credentials/mmh-voice-to-text.json',
        });

- config設定

    config的encoding要注意（注意：encoding和format不是同一件事情）

        const config = {
          encoding: 'MP3',
          sampleRateHertz: 16000,
          languageCode: 'zh-Hant'  //中文
        };

- Format
    - Request格式

        ![Google%20API/_2020-03-12_12.54.16.png](Google%20API/_2020-03-12_12.54.16.png)

        - 測試用音樂檔案

            [Google%20API/test.mp3](Google%20API/test.mp3)

        - 注意：只支援MP3檔案
    - Response

            {
                "success": true,
                "message": "測試測試快點給我錄音"
            }

## 檔案上傳

- 使用express-fileupload

    const fileUpload = require('express-fileupload');
    app.use(fileUpload({
      createParentPath: true
    }));
    
    
    router.post('/',(req,res)=>{
      console.log(req.files.voice.name); //檔案名字 
    	console.log(req.files.voice.size); //檔案大小
    })