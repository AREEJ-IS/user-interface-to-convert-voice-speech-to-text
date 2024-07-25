# user-interface-to-convert-voice-speech-to-text
## Step 1 : Requirements

- XAMPP : https://www.apachefriends.org
- VS code : https://code.visualstudio.com/download
- 
## Step 2 : writing code
````
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Voice to Text Converter</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      background-color: #f2f2f2;
    }

    .container {
      background-color: white;
      padding: 20px;
      border-radius: 5px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      text-align: center;
      width: 600px;
    }

    h1 {
      margin-top: 0;
    }

    .controls {
      display: flex;
      justify-content: center;
      margin-bottom: 20px;
    }

    button {
      background-color: #4CAF50;
      color: white;
      border: none;
      padding: 10px 20px;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 16px;
      margin: 0 10px;
      cursor: pointer;
      border-radius: 5px;
    }

    textarea {
      width: 100%;
      height: 200px;
      font-size: 16px;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      resize: none;
    }

    #status {
      margin-top: 10px;
      font-style: italic;
      color: #888;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Voice to Text Converter</h1>
    <div class="controls">
      <button id="startRecording">Start Recording</button>
      <button id="stopRecording" disabled>Stop Recording</button>
      <button id="saveToDatabase" disabled>Save to Database</button>
    </div>
    <textarea id="textOutput" placeholder="Text will be displayed here"></textarea>
    <div id="status"></div>

    <script>
      const textOutput = document.getElementById('textOutput');
      const startRecordingButton = document.getElementById('startRecording');
      const stopRecordingButton = document.getElementById('stopRecording');
      const saveToDatabaseButton = document.getElementById('saveToDatabase');
      const statusDiv = document.getElementById('status');

      let recognition;

      // Check if the browser supports the Web Speech API
      if ('webkitSpeechRecognition' in window) {
        recognition = new webkitSpeechRecognition();
        recognition.continuous = true;
        recognition.interimResults = true;

        recognition.onresult = (event) => {
          let transcript = '';
          for (let i = event.resultIndex; i < event.results.length; i++) {
            if (event.results[i].isFinal) {
              transcript += event.results[i][0].transcript;
            }
          }
          textOutput.value = transcript;
        };

        recognition.onstart = () => {
          statusDiv.textContent = 'Recording...';
          startRecordingButton.disabled = true;
          stopRecordingButton.disabled = false;
          saveToDatabaseButton.disabled = true;
        };

        recognition.onend = () => {
          statusDiv.textContent = '';
          startRecordingButton.disabled = false;
          stopRecordingButton.disabled = true;
          saveToDatabaseButton.disabled = false;
        };

        startRecordingButton.addEventListener('click', () => {
          recognition.start();
        });

        stopRecordingButton.addEventListener('click', () => {
          recognition.stop();
        });

        saveToDatabaseButton.addEventListener('click', () => {
          // Simulating saving the text to a database
          console.log('Saving text to database:', textOutput.value);
          statusDiv.textContent = 'Text saved to database.';
        });
      } else {
        textOutput.value = 'Your browser does not support the Web Speech API.';
        startRecordingButton.disabled = true;
        stopRecordingButton.disabled = true;
        saveToDatabaseButton.disabled = true;
      }
    </script>
  </div>
</body>
</html>

````
## Step 3 : run and test code 

<img width="1440" alt="Screen Shot 2024-07-25 at 6 19 10 AM" src="https://github.com/user-attachments/assets/92b8edc2-7059-42ca-9993-fff380b1d848">


Click on the Start Recording button


<img width="1440" alt="Screen Shot 2024-07-25 at 6 19 19 AM" src="https://github.com/user-attachments/assets/692d4e65-8ec3-4241-89ce-741df2c7fb4a">


Notice that he starts recording what I say

If you want to stop, click on the Stop Recording button


## Step 4 : The result

Note that he wrote the audio recording. If you want to save it to the database, click the save button



<img width="1440" alt="Screen Shot 2024-07-25 at 6 21 44 AM" src="https://github.com/user-attachments/assets/7ece8a89-142a-4dd8-a307-b224dbac6ed1">

