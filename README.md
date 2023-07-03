package kanban;

import javax.swing.JOptionPane;

/**
 *
 * @author YAYA.AI
 */
public class Login {
    //variables
    private String usr;
    private String pass;
    private String fName;
    private String lName;
    private boolean loggedIn;

    //getter and setter method
    public String getUsr() {
        return usr;
    }

    public void setUsr(String usr) {
        this.usr = usr;
    }

    public String getPass() {
        return pass;
    }

    public void setPass(String pass) {
        this.pass = pass;
    }

    public String getFName() {
        return fName;
    }

    public void setFName(String fName) {
        this.fName = fName;
    }

    public String getLName() {
        return lName;
    }

    public void setLName(String lName) {
        this.lName = lName;
    }

    //check that username has the correct format
    public boolean  checkUsrName() {
        if (usr.contains("_") && usr.length() <= 5) {
            return true;
        } else {
            return false;
        }
    }

    // check if password meets the required standards
    public boolean checkPassComplexity() {
        boolean hasUpper = false;
        boolean hasNum = false;
        boolean hasSpecial = false;

        for (char c : pass.toCharArray()) {
            if (Character.isUpperCase(c)) {
                hasUpper = true;
            } else if (Character.isDigit(c)) {
                hasNum = true;
            } else if (!Character.isLetterOrDigit(c)) {
                hasSpecial = true;
            }
        }
        return pass.length() >= 8 && hasUpper && hasNum && hasSpecial;
    }

    //register user with the provided username and password
    public String registerUser() {
        if (!checkUsrName()) {
            return "Invalid username format. Please make sure your username contains an underscore and is no more than 5 characters.";
        } else if (! checkPassComplexity()) {
            return "Invalid password format. Please make sure your password is at least 8 characters long, includes an uppercase letter, a number, and a special character.";
        } else {
            return "Registration is successful! You can login now!";
        }
    }

    // login the user by verifying the entered username and password 
    public boolean loginUser() {
        String inputUsr = JOptionPane.showInputDialog("Enter your username:");
        String inputPass = JOptionPane.showInputDialog("Enter your password:");
        
        if (inputUsr.equals(usr)&& inputPass.equals(pass)) {
            loggedIn = true;
            return true;
        } else {
            return false;
        }
    }

    //return login status and welcome msg for user
    public String returnLoginStatus() {
        if (loginUser()) {
            return "Welcome " + fName + " " + lName + "! Your login is successful.";
        } else {
            return "Incorrect username or password. Please try again.";
        }
    }
    // user is currently logged in
    public boolean isLoggedIn(){
        return loggedIn;
    }
    
}
