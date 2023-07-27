# Cobra CLI
Cobra is a popular and widely used library in the Go (Golang) programming language for building powerful and flexible command-line applications.

### Root Command:
- In the context of the Cobra library in Go (Golang), the "root command" refers to the top-level command in a CLI application. It serves as the entry point to the application, and other subcommands and flags can be associated with it.
- When building a CLI application using Cobra, you start by defining the root command. The root command can have its own set of flags and actions, and it can also have subcommands, each with their own set of flags and actions. This hierarchical structure allows you to organize and modularize your CLI application in a clean and user-friendly manner.
- For example, in the following code snippet, `rootCmd` is the root command:
```GO
package main

import (
	"fmt"
	"github.com/spf13/cobra"
)

func main() {
	var rootCmd = &cobra.Command{
		Use:   "myapp",
		Short: "My CLI application",
		Run: func(cmd *cobra.Command, args []string) {
			fmt.Println("Hello from the root command!")
		},
	}

	if err := rootCmd.Execute(); err != nil {
		fmt.Println(err)
	}
}
```
- In this example, the `rootCmd` represents the root command with the name "myapp". When you run the CLI application using the command `myapp`, the function specified in the `Run` field of the rootCmd will be executed, and it will print "Hello from the root command!" to the console.
- You can add subcommands to the root command by calling the `rootCmd.AddCommand(subCmd)` method, where `subCmd` is another `cobra.Command` representing a subcommand. Subcommands can have their own unique functionality, flags, and arguments.
- Using the hierarchical structure of the root and subcommands, you can create complex CLI applications with a clear and organized command structure, making it easier for users to interact with your application from the command line.

### Subcommand:
- In the context of CLI (Command-Line Interface) applications, a "subcommand" is a command that is part of a larger command-line tool or application. Subcommands are used to provide different functionalities or operations that can be performed by the main CLI tool.
- Let's take an example of a version control system (like Git) to better understand subcommands. In Git, the main command is "git", and it has several subcommands, each serving a specific purpose. Some common Git subcommands are:
  - git commit: Used to record changes to the repository.
  - git push: Used to upload local changes to a remote repository.
  - git pull: Used to fetch and merge changes from a remote repository to the local repository.
  - git clone: Used to create a copy of a remote repository on the local machine.
- Each of these subcommands has its own set of options, arguments, and behavior, making it a distinct operation within the Git CLI tool.
- Similarly, when building CLI applications using the Cobra library in Go (Golang), you can define subcommands for the root command. These subcommands can have their own unique functionality, flags, and arguments. They provide a way to organize and modularize the CLI application, allowing users to invoke different functionalities based on the subcommand they choose.
- Here's an example of how you can define a subcommand using Cobra in Go:
````GO
package main

import (
	"fmt"
	"github.com/spf13/cobra"
)

func main() {
	var rootCmd = &cobra.Command{Use: "app"}

	var subCmd = &cobra.Command{
		Use:   "subcommand",
		Short: "A subcommand example",
		Run: func(cmd *cobra.Command, args []string) {
			fmt.Println("This is a subcommand!")
		},
	}

	rootCmd.AddCommand(subCmd)

	if err := rootCmd.Execute(); err != nil {
		fmt.Println(err)
	}
}
````
- In this example, we defined a root command named "app". We also defined a subcommand named "subcommand" and associated it with the root command using rootCmd.AddCommand(subCmd). When the CLI application is run with the command app subcommand, it will execute the function specified in the Run field of the subCmd, and it will print "This is a subcommand!" to the console.
- Further Reference: https://github.com/tapojit047/cobra-cli

