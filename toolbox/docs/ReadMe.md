February 20th 2024
NOTE: GITHUB:
cd _cli_
git push


Execution Commands:

go build main.go
go run main.go net



How To Write Beautiful Golang CLI
author: Cloud Native Skunkworks (30:20)
reference CLI from author:
NOTE: One of many difference references on building a CLI
github.com/AlexsJones/cli

START: step-by-step instructions for creating a CLI from tutorial

mkdir toolbox
cd toolbox

go mode init toolbox
OR: (optional method, both work the same) (2:50)
go mod init github.com/AlexsJones/toolbox

NEXT: Download the cobra cli
visit site: https://github.com/spf13/cobra
download:
import "github.com/spf13/cobra"

NOTE: Before continuing make sure to have your GOPATH set up if not follow this quick tutorial video:
YouTube: Downloading Go and Setting up your PATH from Scratch!
Author: Ben Davis (4:49)

echo $GOPATH

NOTE: Your GOPATH is located within the home directory which is the root from where you start when you first cd
Type the following in order to begin from the root directory: ($HOME directory)
ls ~/go/bin/

NOTE: To set up your path type the following command:
export GOBIN=~/go/bin/
export $PATH=$PATH:$GOBIN

NEXT: (terminal command) (4:00 / 30:20)
cobra-cli
cobra-cli init
cobra-cli init toolbox

NOTE: make sure you have the following and no duplicates: (5:15)
main directory: toolbox
directory-files:
go.mod
go.sum
LICENSE
main.go
sub-directory: cmd
sub-directory-file: root.go

NEXT: Make sure you do not have duplicate folders or files. You may accidental have 2 toolbox folders with duplicate files. If so deleted the lowest nested files and directory and leave the files and directory which are closes to the parent untouched. After files are in order run to test the files integrity.
go run main.go

NOTE: With Cobra CLI you can write commands (5:55)
First, we need to relabel our folder(s) (7:00)
-> cmd(folder)
--> net(create, subfolder, "child to cmd")
---> ping.go (ping.go located within the net directory)
---> net.go (Eventually you'll move the net.go file into net directory at a much later time (10:34))
-->info(create, subfolder, "child to cmd)
->cobra-cli add ping (7:30) (file, create file, "file within the toolbox cmd folder")
cobra-cli add net (8:00) create net file nested within the cmd folder and create ping.go file nested within the net folder(8:00)
net.go (in file write)
NOTE: write the following into the net.go file: (8:55 / 9:30)


--------------------------------------------------------------------------------------------

NOTE: below is the net.go (file)

package net

import {
    "github.com/spf13/cobra"
}

var NetCmd = &cobra.Command {
    Use: "net",
    Short: "Net is a palette that contains network based commands.",
    Long: ``,
    Run: func(cmd *cobra.Command, args []string) {
        cmd.Help()
    },
}

func init() {

}


---------------------------------------------------------------------------------------------------


NOTE: below is the root.go file write the follow function (9:25)
root.go


package cmd

import (
	"os"
	"github.com/spf13/cobra"
    "github.com/AlexsJones/toolbox/cmd/net"    // add this import to support your func (10:10)
)


func addSubcommandPalettes() { //Here you create the function
    rootCmd.AddCommand(NetCmd)
}

// the func init() already exist within this file you are using this as a placeholder.
func init() {
    rootCmd.Flags().BoolP("toggle", "t", false, "Help message for toggle")

    addSubcommandPalettes() //Here you invoke the addSubcommandPalettes() within the init() function for execution.
}



-------------------------------------------------------------------------------------------

ping.go file: (11:55)



/*
Copyright © 2024 NAME HERE <EMAIL ADDRESS>
*/
package net

import (
	"github.com/spf13/cobra"
)

var (
	urlPath string
)


// pingCmd represents the ping command
var pingCmd = &cobra.Command{
	Use:   "ping",
	Short: "A brief description of your command",
	Long: `A longer description that spans multiple lines and likely contains examples
and usage of using your command. For example:

Cobra is a CLI library for Go that empowers applications.
This application is a tool to generate the needed files
to quickly create a Cobra application.`,
	Run: func(cmd *cobra.Command, args []string) {
		fmt.Println("ping called")
	},
}

func init() {

    pingCmd.Flags().StringVarP(&urlPath,"url", "u", "", "The url to ping")

	// Here you will define your flags and configuration settings.

    NetCmd.addCommand(pingCommand) //(12:25)


	// Cobra supports Persistent Flags which will work for this command
	// and all subcommands, e.g.:
	// pingCmd.PersistentFlags().String("foo", "", "A help for foo")

	// Cobra supports local flags which will only run when this command
	// is called directly, e.g.:
	// pingCmd.Flags().BoolP("toggle", "t", false, "Help message for toggle")
}

Test code in Terminal: (12:00)
go build main.go
go run main.go net
./toolbox net -h
./toolbox net ping -h




STOP!!! / PAUSED (15:00)
