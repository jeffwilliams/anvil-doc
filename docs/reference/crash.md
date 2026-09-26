# Anvil Crashes

Ideally Anvil should not crash, but occasionally it could due to a coding error. In the case of a crash Anvil will try and write a few files to the current directory to help a developer find the cause of the crash:

  * a file named `anvil.panic` that contains a stacktrace and brief cause of the crash
  * a file named `anvil.panic-logs` that contains recent internal logs 
  * a file named `anvil.panic-gortns` that contains stacktraces of all goroutines






