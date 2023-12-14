# Capstone Project IV - Compulsory Task

# This program is designed for use in a small business.
# It works to manage tasks assigned to team members.
# =====importing libraries===========
# Importing necessary modules
import os
import datetime
from datetime import date


# Function to authenticate user
def authenticate_user(username, password):
    try:
        # Define the relative file path for the user information
        relative_path = os.path.join(
            "C:/Users/Blue Chelsea/Documents/capstone project/user.txt"
        )
        # Open the user file in read mode and check for username and password matches
        with open(relative_path, "r") as file:
            for line in file:
                parts = line.strip().split(",")  # Split the line based on comma
                stored_username = parts[0].strip()  # Extract stored username
                stored_password = parts[1].strip()  # Extract stored password
                # Check if the provided username and password match the stored values
                if username == stored_username and password == stored_password:
                    return True  # Return True if authentication is successful
            return False  # Return False if no match is found
    except FileNotFoundError:
        return "file not found!!!"  # Handle the case if the file is not found


def add_task():

    # Prompt user to enter task details
    username = input("Enter the username of the person the task is assigned to: ")
    title = input("Enter the title of the task: ")
    description = input("Enter the description of the task: ")
    # Using the previously imported datetime module to calculate the current date
    current_date = datetime.date.today()  # Get the current date
    # Prompt user to enter the due date of the task
    due_date = input("Enter the due date of the task (format 'YYYY-MM-DD'): ")
    try:
        # Define the file path to the tasks file
        relative_path = os.path.join(
            "C:/Users/Blue Chelsea/Documents/capstone project/tasks.txt"
        )  # Define the relative file path for the tasks

        # Open the tasks file in append mode and write the task details
        with open(relative_path, "a") as file:
            # Write the task details to the file in the specified format
            file.write(
                f"\n{username}, {title}, {description}, {due_date}, {current_date}, Not completed"
            )
            print(
                "Task added successfully!"
            )  # Notify user about successful task addition
    except FileNotFoundError:
        return "file not found!"  # Handle the case if the file is not found


def view_my_tasks(username):
    try:

        relative_path = os.path.join(
            "C:/Users/Blue Chelsea/Documents/capstone project/tasks.txt"
        )  # Define the relative file path for the tasks

        with open(relative_path, "r") as file:  # Open the tasks file in read mode
            tasks = file.readlines()  # Read all the lines from the file
            username_exists = True
            for task in tasks:  # Iterate through each task in the file
                task_details = task.strip().split(
                    ", "
                )  # Split the task details based on the comma and space
                if (
                    task_details[0] == username
                ):  # Check if the task is assigned to the specified username
                    # Print the task details
                    print(f"Assigned to: {task_details[0]}")
                    print(f"Title: {task_details[1]}")
                    print(f"Description: {task_details[2]}")
                    print(f"Due Date: {task_details[3]}")
                    print(f"current date: {task_details[4]}")
                    print(f"Status: {task_details[5]}")

                    print()
            if not username_exists:
                print("username doesnt exist.")  # If the username doesn't exist

    except Exception as e:
        return "Error occured. please try again."  # Handle any exceptions and display an error message


def display_statistics():

    try:

        relative_path = os.path.join(
            "C:/Users/Blue Chelsea/Documents/capstone project/user.txt"
        )  # Define the relative file path for the user

        with open(relative_path, "r") as user_file:

            total_users = sum(
                1 for _ in user_file
            )  # Count the total number of lines in the user file

        current_dir = os.getcwd()  # Get the current directory

        relative_path = os.path.join(
            "C:/Users/Blue Chelsea/Documents/capstone project/tasks.txt"
        )  # Define the relative file path for the tasks

        with open(relative_path, "r") as task_file:  # Open the tasks file in read mode
            total_tasks = sum(
                1 for _ in task_file
            )  # Count the total number of lines in the task file

        # Print the total number of users and total number of tasks
        print(f"Total number of users: {total_users}")
        print(f"Total number of tasks: {total_tasks}")

    except FileNotFoundError:  # Handle the case when the file is not found
        print(
            "zero tasks added"
        )  # Print a message indicating that zero tasks were added


# User authentication loop
while True:
    username = input("Enter your username: ")  # Prompt the user to enter their username
    password = input("Enter your password: ")  # Prompt the user to enter their password
    if authenticate_user(
        username, password
    ):  # Check if the user's credentials are authenticated
        print("Login successful!")  # Print a success message
        break  # Exit the authentication loop
    else:
        print(
            "Invalid username or password. Please try again."
        )  # Print an error message


while True:
    # Present the menu to the admin and make sure that the user input is converted to lower case
    if username == "admin" and password == "adm1n":  # Check if the user is the admin

        menu = input(
            """Select one of the following options:
    r - register a user
    a - add task
    va - view all tasks
    vm - view my tasks
    ds - display statistics
    e - exit
    : """
        ).lower()  # Prompt the admin to select an option and convert the input to lower case

        if menu == "r":
            # User registration

            new_username = input(
                "Enter a new username: "
            )  # Prompt to enter a new username
            new_password = input(
                "Enter a new password: "
            )  # Prompt to enter a new password
            confirm_password = input(
                "Confirm the password: "
            )  # Prompt to confirm the password
            if new_password == confirm_password:  # Check if the passwords match
                relative_path = os.path.join(
                    "C:/Users/Blue Chelsea/Documents/capstone project/user.txt"
                )  # Create a relative path for the user file

                with open(
                    relative_path, "a"
                ) as file:  # Open the user file in append mode
                    file.write(f"\n{new_username}, {new_password}")
                    # Write the new user's credentials to the file
                    print("User registered successfully!")
                    # Print a success message for user registration
            else:
                pass
                print("Passwords do not match. User registration failed.")
                # Print an error message for password mismatch

        elif menu == "a":
            # Add task
            pass
            add_task()  # Call the add_task function to add a new task

        elif menu == "va":
            # View all tasks
            pass
            try:
                # Open and read the tasks from the tasks.txt file
                # create a relative path
                relative_path2 = os.path.join(
                    "C:/Users/Blue Chelsea/Documents/capstone project/tasks.txt"
                )
                with open(
                    relative_path2, "r+"
                ) as file:  # Open the tasks file in read mode

                    tasks = (
                        file.readlines()
                    )  # Read all the lines from the file into a list
                    for task in tasks:  # Iterate through each task in the list
                        task_details = task.strip().split(
                            ", "
                        )  # Split the task details using comma and space as the delimiter
                        # Print the task details
                        print(f"Assigned to: {task_details[0]}")
                        print(f"Title: {task_details[1]}")
                        print(f"Description: {task_details[2]}")
                        print(f"Due Date: {task_details[3]}")
                        print(f"current date: {task_details[4]}")
                        print(f"Status: {task_details[5]}")
                        print()
                print("--------------------------------------------")
                print("End of Tasks.")  # Print a message indicating the end of tasks

            except IndexError:
                print("---------------------------------------------")

            except FileNotFoundError:
                print(
                    "file not found!!!"
                )  # Print an error message if the file is not found
        elif menu == "vm":  # View my tasks
            pass
            username = input(
                "Enter your username: "
            )  # Prompt the user to enter their username
            view_my_tasks(
                username
            )  # Call the view_my_tasks function with the provided username
        elif menu == "ds":  # Display statistics
            pass
            display_statistics()  # Call the display_statistics function to show statistics
        elif menu == "e":
            print("Goodbye!!!")  # Print a farewell message
            exit()  # Exit the program

        else:  # Handling invalid input
            print("You have made entered an invalid input. Please try again")
            # Print an error message for invalid input
    else:  # Handling menu options for non-admin users

        menu = input(
            """Select one of the following options:

r - register user
a - add task
va - view all tasks
vm - view my tasks
e - exit

:"""
        ).lower()  # Prompt the user to select an option and convert the input to lowercase
        if menu == "r":  # Register user (only admin)
            print("only admin can register new users")
            # Print a message indicating that only admin can register new users
        elif menu == "a":
            # Add task
            pass
            add_task()  # Call the add_task function to add a new task

        elif menu == "va":
            # View all tasks
            pass
            try:
                # Open and read the tasks from the tasks.txt file

                # create a relative path
                relative_path2 = os.path.join(
                    "C:/Users/Blue Chelsea/Documents/capstone project/tasks.txt"
                )
                with open(
                    relative_path2, "r+"
                ) as file:  # Open the tasks file in read mode

                    tasks = (
                        file.readlines()
                    )  # Read all the lines from the file into a list
                    for task in tasks:  # Iterate through each task in the list
                        task_details = task.strip().split(
                            ", "
                        )  # Split the task details using comma and space as the delimiter
                        # Print the task details
                        print(f"Assigned to: {task_details[0]}")
                        print(f"Title: {task_details[1]}")
                        print(f"Description: {task_details[2]}")
                        print(f"Due Date: {task_details[3]}")
                        print(f"current date: {task_details[4]}")
                        print(f"Status: {task_details[5]}")
                        print()
                print("--------------------------------------------")
                print("End of Tasks.")  # Print a message indicating the end of tasks
                break
            except IndexError:
                print("---------------------------------------------")

            except FileNotFoundError:
                print(
                    "file not found!!!"
                )  # Print an error message if the file is not found
        elif menu == "vm":  # View my tasks
            pass
            username = input(
                "Enter your username: "
            )  # Prompt the user to enter their username
            view_my_tasks(
                username
            )  # Call the view_my_tasks function with the provided username

        elif menu == "e":
            print("Goodbye!!!")  # Print a farewell message
            exit()  # Exit the program

        else:  # Handling invalid input
            print("You have made entered an invalid input. Please try again")
            # Print an error message for invalid input
