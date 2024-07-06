---
layout: post
title: "Interactive Message Generator"
date: 2024-07-06 12:00:00 -0500
categories: [Programming, Fun]
tags: [python, interactive-script, message-generator]
---

# Interactive Message Generator

Today, we're exploring a fun and interactive message generator script that I've developed. This Python script allows users to create personalized messages with a cool typing effect, making it perfect for romantic notes, friendly messages, or custom greetings!

## Try It Yourself!

You can run this message generator directly in your browser using the interactive Repl below:

<iframe height="800px" width="100%" src="https://repl.it/@YourUsername/MessageGenerator?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Just click "Run" and follow the prompts in the console to generate your message!

## How It Works

The script performs the following steps:

1. Asks for the name of the recipient.
2. Offers a choice between pre-defined message templates (romantic or friendly) or a custom message.
3. Generates the message based on the user's choice.
4. Displays the message with a cool typing effect.

## Key Features

- Choice of romantic or friendly pre-defined messages
- Option to create a custom message
- Simulated typing effect for a more interactive display
- Easy to use and customize

## The Code

Here's the Python script for our message generator:

```python
import time

def display_message(message):
    """
    Simulate typing effect for a more interactive display.
    """
    for char in message:
        print(char, end='', flush=True)
        time.sleep(0.05)  # Adjust the speed of typing effect
    print("\n")

def select_message(name):
    """
    Select a predefined message or allow the user to create a custom one.
    """
    print("Choose a message template:")
    print("1. Romantic")
    print("2. Friendly")
    print("3. Custom")
    choice = input("Enter the number of your choice: ")
    if choice == '1':
        message = (
            f"Dear {name},\n\n"
            "I wanted to let you know that...\n\n"
            "I love you with all my heart!\n\n"
            "Forever yours,\nKareem\n"
        )
    elif choice == '2':
        message = (
            f"Hey {name},\n\n"
            "Just wanted to say...\n\n"
            "You're an amazing friend!\n\n"
            "Cheers,\nKareem\n"
        )
    elif choice == '3':
        custom_message = input("Enter your custom message: ")
        message = f"Dear {name},\n\n{custom_message}\n\nBest regards,\nKareem\n"
    else:
        print("Invalid choice. Using default message.")
        message = (
            f"Dear {name},\n\n"
            "I wanted to let you know that...\n\n"
            "I love you with all my heart!\n\n"
            "Forever yours,\nKareem\n"
        )
    return message

def main():
    """
    Main function to handle user input and display the message.
    """
    # Ask for user input
    name = input("Enter the name of your beloved: ")
    
    # Get the selected message
    message = select_message(name)
    
    # Display the message with a typing effect
    display_message(message)

# Entry point of the script
if __name__ == "__main__":
    main()