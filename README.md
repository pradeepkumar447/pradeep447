# pradeep447
import json
import os

# File to store tasks
FILE_NAME = "tasks.json"


# Load tasks from file
def load_tasks():
    if not os.path.exists(FILE_NAME):
        return []
    with open(FILE_NAME, "r") as file:
        return json.load(file)


# Save tasks to file
def save_tasks(tasks):
    with open(FILE_NAME, "w") as file:
        json.dump(tasks, file, indent=4)


# Display tasks
def view_tasks(tasks):
    if not tasks:
        print("\nNo tasks available.\n")
        return

    print("\n---- Your To-Do List ----\n")
    for idx, task in enumerate(tasks, 1):
        status = "✔ COMPLETED" if task["completed"] else "⏳ PENDING"
        print(f"{idx}. {task['task']}  -->  {status}")
    print()


# Add new task
def add_task(tasks):
    task_name = input("Enter task: ")
    tasks.append({"task": task_name, "completed": False})
    print("Task Added Successfully!")


# Mark task as completed
def complete_task(tasks):
    view_tasks(tasks)
    try:
        num = int(input("Enter task number to mark complete: "))
        tasks[num - 1]["completed"] = True
        print("Task Marked as Completed!")
    except:
        print("Invalid choice!")


# Update an existing task
def update_task(tasks):
    view_tasks(tasks)
    try:
        num = int(input("Enter task number to update: "))
        new_name = input("Enter updated task: ")
        tasks[num - 1]["task"] = new_name
        print("Task Updated Successfully!")
    except:
        print("Invalid choice!")


# Delete a task
def delete_task(tasks):
    view_tasks(tasks)
    try:
        num = int(input("Enter task number to delete: "))
        tasks.pop(num - 1)
        print("Task Deleted Successfully!")
    except:
        print("Invalid choice!")


# Main program
def main():
    tasks = load_tasks()

    while True:
        print("""
========= TO-DO LIST MENU =========
1. View Tasks
2. Add Task
3. Update Task
4. Mark Task as Completed
5. Delete Task
6. Save & Exit
===================================
""")

        choice = input("Enter your choice: ")

        if choice == '1':
            view_tasks(tasks)
        elif choice == '2':
            add_task(tasks)
        elif choice == '3':
            update_task(tasks)
        elif choice == '4':
            complete_task(tasks)
        elif choice == '5':
            delete_task(tasks)
        elif choice == '6':
            save_tasks(tasks)
            print("Tasks Saved. Exiting...")
            break
        else:
            print("Invalid input! Please try again.")


if __name__ == "__main__":
    main()
