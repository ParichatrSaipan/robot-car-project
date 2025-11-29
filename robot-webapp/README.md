# robot-car-project

## Getting Started Guide for Developing the robot-car-project webapp on Raspberry Pi 4

1. **Open Terminal**: Start by opening the Terminal program to use various commands

2. **Use Basic Commands**:

   - **`ls`**: Use to display all files and folders in the current location
     ```bash
     ls
     ```

   - **`cd <directory-name>`**: Use to change to another directory, for example, changing to the `robot-car-project` folder
     ```bash
     cd robot-car-project
     ```

   - **`cd ..`**: Use to go back to the previous directory
     ```bash
     cd ..
     ```

   - **`pwd`**: Use to display the current location (path) in the system's directory structure
     ```bash
     pwd
     ```
     Example output when using `pwd` command and pressing Enter:
     ```bash
     /var/www/html/robot-car-project/robot-webapp
     ```

   ## SSH via VSCode

    1. Click as shown in the image below

    ![image](../readme-picture/Screenshot%202567-11-02%20at%2020.20.55.png)

    2. Click Remote-SSH: Connect to Host... as shown in the image below

    ![image](../readme-picture/Screenshot%202567-11-02%20at%2020.21.53.png)

    3. Type password and press Enter
    ```bash
     earnpan
     ```
    4. Click Open Folder as shown in the image below

    ![image](../readme-picture/Screenshot%202567-11-02%20at%2020.23.20.png)

    5. Click Choose Folder with the following path
    ```bash
     /var/www/html/robot-car-project/robot-webapp
     ```
    6. Edit files normally

    7. Save file by pressing `ctrl + shift + p` in VSCode, then type `save as root` and press Enter

    8. `cd` to the `robot-webapp` folder and type the command below
        ```bash
        npm run build
        ```



