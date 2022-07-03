# AudioBook-MP3
complete Audiobook code with SimplePyGUI
This are two different codes which i practiced and i have merge them to create Audiobook with MP3 GUI
Please do share and comments what i can do to expand this.
i a still learning at a begginer level.
Any help and recommendations are welcome.







import PyPDF2
import pyttsx3
import PySimpleGUI as sg

file_name = 'Oop.pdf'
reading_speed = 100 
voice_id = 1

engine = pyttsx3.init()
fileObj = open(file_name, 'rb')

pdfReader = PyPDF2.PdfFileReader(fileObj)
pages_num = pdfReader.numPages

print("press CTRL + C to stop!")

for num in range(pages_num):
    pageObj = pdfReader.getPage(num)
    text = pageObj.extractText()


controls = [sg.Button("Play"), sg.Button("Pause"), sg.Button("Stop")]

layout = [[sg.FileBrowse(key = "file_name", enable_events=True)], controls]
window = sg.Window("MP3 Player", layout)

while True:
    event,values = window.read()
    if event == "OK" or event == sg.WIN_CLOSED:
        break
    if event == "-MP3-":
       player = file_name.MediaPlayer(values["file_name"])

    if event == "play" and player is not None:
        player.play()

    if event == "Pause" and player is not None:
        player.pause()

    if event == "Stop" and player is not None:
        player.stop()

    voices = engine.getProperty('voice')
    engine.setProperty('voices',[voice_id])
    engine.say(f"Page {num + 10}" +  text)
    engine.setProperty('rate', reading_speed)
    engine.runAndWait()

window.close()

fileObj.close()
