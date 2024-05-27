# CodeAlpha_To-Do-List-Application

#include <iostream>
#include <vector>
#include <string>

class Task {
public:
    Task(const std::string& desc) : description(desc), completed(false) {}

    void markCompleted() {
        completed = true;
    }

    bool isCompleted() const {
        return completed;
    }

    std::string getDescription() const {
        return description;
    }

private:
    std::string description;
    bool completed;
};

void addTask(std::vector<Task>& tasks, const std::string& description) {
    tasks.emplace_back(description);
    std::cout << "Task added: " << description << "\n";
}

void addTaskFromUser(std::vector<Task>& tasks) {
    std::string description;
    std::cout << "Enter the task description: ";
    std::getline(std::cin, description);
    addTask(tasks, description);
}

void markTaskCompleted(std::vector<Task>& tasks) {
    int taskNumber;
    std::cout << "Enter the task number to mark as completed: ";
    std::cin >> taskNumber;
    std::cin.ignore();  // To clear the newline character from the input buffer

    if (taskNumber > 0 && taskNumber <= tasks.size()) {
        tasks[taskNumber - 1].markCompleted();
        std::cout << "Task marked as completed!\n";
    } else {
        std::cout << "Invalid task number!\n";
    }
}

void viewTasks(const std::vector<Task>& tasks) {
    if (tasks.empty()) {
        std::cout << "No tasks available.\n";
        return;
    }

    std::cout << "Current tasks:\n";
    for (size_t i = 0; i < tasks.size(); ++i) {
        std::cout << i + 1 << ". " << tasks[i].getDescription();
        if (tasks[i].isCompleted()) {
            std::cout << " [Completed]";
        }
        std::cout << "\n";
    }
}

void showMenu() {
    std::cout << "\nTo-Do List Application\n";
    std::cout << "1. Add task\n";
    std::cout << "2. Mark task as completed\n";
    std::cout << "3. View tasks\n";
    std::cout << "4. Exit\n";
    std::cout << "Enter your choice: ";
}

int main() {
    std::vector<Task> tasks;

    // Adding initial tasks for demonstration
    addTask(tasks, "Buy groceries");
    addTask(tasks, "Complete C++ project");
    addTask(tasks, "Call mom");

    int choice;

    do {
        showMenu();
        std::cin >> choice;
        std::cin.ignore();  // To clear the newline character from the input buffer

        switch (choice) {
            case 1:
                addTaskFromUser(tasks);
                break;
            case 2:
                markTaskCompleted(tasks);
                break;
            case 3:
                viewTasks(tasks);
                break;
            case 4:
                std::cout << "Exiting the application.\n";
                break;
            default:
                std::cout << "Invalid choice! Please try again.\n";
        }
    } while (choice != 4);

    return 0;
}

