## Thread execution 
It seems that when a java application or installer executes via azure devops pipeline or other remote processes it exits before completing its main task.
The difference between these two types of threads is that if the JVM determines that the only threads running in an application are daemon threads (i.e., there are no user threads), the Java runtime closes down the application. 
On the other hand, if at least one user thread is alive, the Java runtime won't terminate your application.

To get around this i found that using a Invoke-Command -ComputerName "localhost" -ScriptBlock {<your script>} Exit-PSSession solved the problem.
This issue took me a quite of trial and error to figure out why it was happening since the process would work just fine when running locally via RDP.
Since the pipeline was using the same user as i was logging into the machine i couldn't figure out why it didn't work in devops.
  
  
