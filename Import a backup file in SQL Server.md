# Import a backup file in SQL Server

A backup file with the extension **.bak** can be opened in SQL Server Management Studio to obtain data. The steps below describe the process.

1. Download and install SQL Server
  
2. Click Start, select All Programs, click Microsoft SQL Server 2022, and select SQL Server Management Studio.  
--> This will bring up the Connect to Server dialog box.  
Please ensure that the Server name YourServerName and that Authentication is set to Windows Authentication.  
Click Connect.

3. Right-click **Databases** and select **Restore Database**.  
--> This will bring up the Restore Database window.

4. On the **Restore Database** screen, select Device and click the "..." box.  
--> This will bring up the Select backup devices screen.

5. On the **Specify Backup** screen, click **Add**.  
--> This will bring up the Locate Backup File screen.

6. Copy the default file path for backup files in SQL Server. Then, open a new file explorer (using the shortcut **CTRL + N**), paste the file path and press **Enter**.  
--> This shows the backup folder.

7. On another file explorer window, copy the backup file you want to restore and put it in the SQL Server default file path. You can now close the file explorer windows opened.  

8. Go back to the **Locate Backup File** screen and click the **Refresh** button.  
--> This brings the backup file you just added.

9. Select the file name.  
--> This automatically appears in the File name box at the bottom.

10. Click **OK**  
--> This closes the Locate Backup File screen.

11. Click OK to close the Select Backup devices screen. 

12. On the Restore Database window, you will see that your database is automatically added and there is a check box under Restore. Click **OK**  
--> This shows a pop-up window saying that your database was restored successfully.

13. Your New database is now listed.

<!-- You can also watch this [video](https://www.youtube.com/watch?v=kQs0Uywl4_c&list=PLh2dQuuw5qTUIREUqH5zM2fPcxdJanT5r) for directions. -->


</br></br>
Author: [Edwige Songong](https://github.com/Songonge)
