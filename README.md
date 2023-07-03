# Kanban
A kanban board is a visual tool with columns representing stages of work. Cards move across columns (To Do, In Progress, Done) as tasks progress. It helps teams track and prioritize work, promoting transparency and collaboration.
This is the login and tasks features only!

/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package kanban;

import javax.swing.JComboBox;
import javax.swing.JOptionPane;

/**
 *
 * @author YAYA.AI
 */
public class Kanban {
        //method to create a new task
    
     public static task createTask() {
             
        //prompt user for task details
        String taskName = JOptionPane.showInputDialog("Add login feature:");
        String taskDescription = JOptionPane.showInputDialog("Please enter a task description of less than 50 characters");
        String developerDetails = JOptionPane.showInputDialog("Enter the full name of the developer assigned to the task:");
        double taskDuration = Double.parseDouble(JOptionPane.showInputDialog("Enter the task duration in hours:"));
        
        //create a combo box for task status selection
        String[] statusOptions = {"To do","Doing","Done"};
        JComboBox<String> statusComboBox = new JComboBox<>(statusOptions);
        //Show the combo box and get selected status
        JOptionPane.showMessageDialog(null, statusComboBox,"Select task status",JOptionPane.QUESTION_MESSAGE);
        String taskStatus = (String)statusComboBox.getSelectedItem();
        
        //create a new task 
         taskCounter tc = new taskCounter();
         int taskNumber = taskCounter.getNextTaskNumber();
         
         return new task(taskName, taskNumber, taskDescription, developerDetails, taskDuration, taskStatus);

    }
    
        // keep track of task counter
        static class taskCounter{
            private static int taskNumber = 0;
            
            public static int getNextTaskNumber(){
                taskNumber ++; //increment the value of taskNumber
                return taskNumber;
            }
        }
    public static void main(String[] args) {
           Login lo = new Login(); // creating an instance of the class
        task[] tasks = new task[10]; // Array to store tasks

        while (true) { // Looping the menu
            String menuOption = JOptionPane.showInputDialog("Main Menu \n" +
                    "Enter 1 --> Register \n" +
                    "Enter 2 --> Login \n" +
                    "Enter 3 --> Exit \n" +
                    "\n Enter your menu option:");

            int option = Integer.parseInt(menuOption);

            // decisions based onselected menu option
            if (option == 1) {
                // prompt user for registration details
                String username = JOptionPane.showInputDialog("Enter a username:");
                String password = JOptionPane.showInputDialog("Enter a password:");
                String firstName = JOptionPane.showInputDialog("Enter your first name:");
                String lastName = JOptionPane.showInputDialog("Enter your last name:");
                // set registration details using setter method 
                lo.setUsr(username);
                lo.setPass(password);
                lo.setFName(firstName);
                lo.setLName(lastName);

                String registrationMessage = lo.registerUser();
                JOptionPane.showMessageDialog(null, registrationMessage);
            } else if (option == 2) {
                String loginStatus = lo.returnLoginStatus();
                JOptionPane.showMessageDialog(null, loginStatus);

               
                if (lo.isLoggedIn()) {
                    JOptionPane.showMessageDialog(null, "Welcome to EasyKanban!");

                    // an inner menu for add tasks, show report, and quit 
                    while (true) {
                        String innerMenuOption = JOptionPane.showInputDialog("EasyKanban Menu \n" +
                                "Enter 1 --> Add Tasks \n" +
                                "Enter 2 --> Show Report \n" +
                                "Enter 3 --> Quit \n" +
                                "\n Enter your menu option:");

                        int innerOption = Integer.parseInt(innerMenuOption);

                        if (innerOption == 1) {
                            // add tasks to the task array
                            String numTasksStr = JOptionPane.showInputDialog("Enter the number of tasks:");
                            int numTasks = Integer.parseInt(numTasksStr);
                            for (int i = 0; i < numTasks; i++) {
                                task task = createTask();
                                if (task.checkTaskDescription()) {
                                    tasks[i] = task;
                                    JOptionPane.showMessageDialog(null, "Task successfully captured");
                                    JOptionPane.showMessageDialog(null, task.printTaskDetails());
                                } else {
                                    JOptionPane.showMessageDialog(null, "Please enter a task description of less than 50 characters");
                                    i--; // re-prompt for the current task
                                }
                                 int totalHours = task.returnTotalHours(tasks);
                                 String message = "The total hours on the tasks are: " + totalHours;
                                  JOptionPane.showMessageDialog(null, message);
                            }
                        } else if (innerOption == 2) {
                            JOptionPane.showMessageDialog(null, "Coming Soon");
                            
                        } else if (innerOption == 3) {
                            break; // exit inner menu to the main menu
                        } else {
                            JOptionPane.showMessageDialog(null, "Invalid menu option. Try again!!!");
                        }
                    }
                }
            } else if (option == 3) {
                break; // exit main menu and program
            } else {
                JOptionPane.showMessageDialog(null, "Invalid menu option. Try again!!!");
            }
        }
    }
}
