February 20th 2024



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
cd .. (outside of cmd directory)
cobra-cli add net (8:00) net.go file created
NOW:
mkdir net (within the cmd directory)
mv net.go net
NOTE; open the net.go file
package cmd (rename package cmd) (8:30)
package net






