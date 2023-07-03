package kanban;

/**
 *
 * @author YAYA.AI
 */
public class task {
    // variables
    private String taskName;
    private int taskNumber;
    private String taskDescription;
    private String developerDetails;
    private double taskDuration;
    private String taskID;
    private String taskStatus;

    public task(String taskName, int taskNumber, String taskDescription, String developerDetails, double taskDuration, String taskStatus) {
       //constructor to initialize the task objects 
        this.taskName = taskName;
        this.taskNumber = taskNumber;
        this.taskDescription = taskDescription;
        this.developerDetails = developerDetails;
        this.taskDuration = taskDuration;
        this.taskID = createTaskID();// unique task ID
        this.taskStatus = taskStatus;
    }

    // check if task description is less than or equals 50 characters
    public boolean checkTaskDescription() {
        return taskDescription.length() <= 50;
    }

    // create task ID
    public String createTaskID() {
        // get first 2 characters of task name and convert them to uppercase
        String initials = taskName.substring(0, 2).toUpperCase();
        //concatenate the initials, task number and last 3 letters of dev details
        String taskId = initials + ":" + taskNumber + ":" + developerDetails.substring(developerDetails.length() - 3).toUpperCase();
        return taskId;
    }

    // Print the task details 
    public String printTaskDetails() {
        return "Task Status: " + taskStatus + "\nDeveloper Details: " + developerDetails +
                "\nTask Number: " + taskNumber + "\nTask Name: " + taskName +
                "\nTask Description: " + taskDescription + "\nTask ID: " + taskID +
                "\nTask Duration: " + taskDuration + " hours";
    }

    // get the duration for each task
    public double getTaskDuration() {
        return taskDuration;
    }

    // to do/ doing/ done
    public String getTaskStatus() {
        return taskStatus;
    }
    
    // calculate the total hours for an array of tasks
    public static int returnTotalHours(task[] tasks){
        int totalHours = 0;
        //iterte through all taks in the task array
        for(task t : tasks){
            if(t != null){
                //add the task duration to the total hours 
                totalHours += t.getTaskDuration();
            }
        }
        return totalHours;
        }
}

