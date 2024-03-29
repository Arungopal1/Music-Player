# Music-Player

import os
import tkinter.messagebox
from tkinter import *
from tkinter import filedialog
from pygame import mixer

root = Tk()
root.title("Music Player")

mixer.init()  # Initialize the mixer

# Function to add a music file to the playlist
def add_music():
    file = filedialog.askopenfilename()
    playlistbox.insert(END, file)

# Function to delete a selected music file from the playlist
def delete_music():
    selected_song = playlistbox.curselection()
    playlistbox.delete(selected_song[0])

# Function to play the selected music file
def play_music():
    try:
        selected_song = playlistbox.curselection()
        selected_song = int(selected_song[0])
        play_it = playlistbox.get(selected_song)
        mixer.music.load(play_it)
        mixer.music.play()
    except:
        tkinter.messagebox.showerror('File not found', 'Music file could not be found. Please check again.')

# Function to stop the music
def stop_music():
    mixer.music.stop()

# Create frames
leftframe = Frame(root)
leftframe.pack(side=LEFT, padx=30, pady=30)

rightframe = Frame(root)
rightframe.pack(pady=30)

# Create playlist listbox
playlistbox = Listbox(leftframe)
playlistbox.pack()

# Add buttons
addBtn = Button(leftframe, text="Add", command=add_music)
addBtn.pack(side=LEFT, padx=10)

delBtn = Button(leftframe, text="Delete", command=delete_music)
delBtn.pack(side=LEFT, padx=10)

# Add buttons to control music playback
playBtn = Button(rightframe, text="Play", command=play_music)
playBtn.grid(row=0, column=0, padx=10)

stopBtn = Button(rightframe, text="Stop", command=stop_music)
stopBtn.grid(row=0, column=1, padx=10)

# Start the GUI
root.mainloop()
