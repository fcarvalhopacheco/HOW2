# How to install and configure taskwarrior.

## Source 

[Taskwarrior](https://taskwarrior.org/download/)


## Download & Install

1. Download Taskwarrior for `macOS`

- Installs a command-line task management tool that
allows you to manage and track tasks directly from your terminal. Taskwarrior
is known for its simplicity and flexibility.

```sh 
brew install task
```

2. Download Taskwarrior server

- It's used to synchronize tasks across multiple devices. If you're using
Taskwarrior on more than one machine and want to keep your tasks synchronized,
you'll need taskd to handle the server-side of the synchronization process. 

```sh 
brew install taskd
```


<!-- 3. Download Taskshell -->
<!---->
<!-- - installs Taskshell (tasksh), an interactive shell for Taskwarrior. It -->
<!-- provides an immersive environment for managing your tasks and can be useful for -->
<!-- batch operations or when you prefer to work in a dedicated task management -->
<!-- environment. -->
<!---->
<!-- ``` sh  -->
<!-- brew install tasksh: -->
<!-- ``` -->


<!-- 4. Download Timewarrior -->
<!---->
<!---->
<!-- - Timewarrior is a command line time tracking application, which allows you to -->
<!-- record time spent on activities. You may be tracking your time for curiosity, -->
<!-- or because your work requires it. At its simplest, you tell it to start and -->
<!-- stop tracking time ([Timewarrior](https://timewarrior.net/docs/what/)) -->
<!---->
<!-- ```sh  -->
<!-- brew install timewarrior -->
<!-- ``` -->



## Configuration
1. Taskwarrior configuration file


- On your terminal, just type `task`. The program will ask to install the
configuration file at `$HOME/.taskrc`.

- ps. I will create my config (`.taskrc`) file at my `.dotfile` so I can stow
it later.

`.taskrc`: 

```.taskrc
# [Created by task 2.6.2 11/15/2023 07:34:32]
# Taskwarrior program configuration file.
# For more documentation, see https://taskwarrior.org or try 'man task', 'man task-color',
# 'man task-sync' or 'man taskrc'

# Here is an example of entries that use the default, override and blank values
#   variable=foo   -- By specifying a value, this overrides the default
#   variable=      -- By specifying no value, this means no default
#   #variable=foo  -- By commenting out the line, or deleting it, this uses the default

# You can also refence environment variables:
#   variable=$HOME/task
#   variable=$VALUE

# Use the command 'task show' to see all defaults and overrides

# Files
data.location=/Users/fcp/.task

# To use the default location of the XDG directories,
# move this configuration file from ~/.taskrc to ~/.config/task/taskrc and uncomment below

#data.location=~/.local/share/task
#hooks.location=~/.config/task/hooks

# Color theme (uncomment one to use)
#include light-16.theme
#include light-256.theme
#include dark-16.theme
#include dark-256.theme
#include dark-red-256.theme
#include dark-green-256.theme
#include dark-blue-256.theme
#include dark-violets-256.theme
#include dark-yellow-green.theme
#include dark-gray-256.theme
#include dark-gray-blue-256.theme
#include solarized-dark-256.theme
#include solarized-light-256.theme
#include no-color.theme

```

- On terminal, run:

```sh 
mkdir -p .dotfiles/task/
cd ~/.dotfiles
stow task
```



2. Taskwarrior SERVER configuration

**TODO**

## Examples


### Task Structure in Taskwarrior
1. Projects:
- Your first bracketed item, like [HOT], [WHOTS], etc., can directly translate to
Taskwarrior's project field. 

Example: project:HOT

2. ID / Cruise Number:
This can be added as part of the task description or as a tag for easy filtering.
Example: +346

3. "What" Category:
These can also be used as tags in Taskwarrior.
Example: +CTD, +Underway, etc.

4. "Tasks" Category:
Again, use these as tags.
Example: +DataProcessing, +CruisePreparation, etc.

5. Task Description:
Combine all these elements into a clear task description.
Example: "Prepare data processing for HOT cruise 346 [CTD] [DataProcessing]"

### Tips and tricks 

- Taskwarrior allows you to add annotations to tasks, which are essentially notes
or comments. Your detailed notes can be added as annotations to each task. For
example:

1. **Adding Annotations**: 
   - Use annotations for detailed notes or comments.
   - Example:
     ```sh
     task add "Prepare data processing for HOT cruise 346 [CTD] [DataProcessing]" project:HOT +346 +CTD +DataProcessing
     task 1 annotate "This is an important note."
     ```

2. **Viewing Completed Tasks**: 
   - Use `task completed` to view all completed tasks.
     ```sh
     task completed
     ```

3. **Searching for Tags**: 
   - Find tasks using specific tags.
     ```sh
     task +TAG list
     ```

4. **Modifying Completed Tasks**: 
   - To modify a completed task, temporarily revert it to pending, make changes, then mark as done.
     ```sh
     task TASKID modify status:pending
     task TASKID annotate "Additional annotation"
     task TASKID modify entry:'2023-11-15T10:00:00'
     task TASKID modify end:'2023-11-15T16:04:00'
     task TASKID done
     ```

### Additional Examples

1. **Setting Priorities**:
   - Assign priorities to tasks.
     ```sh
     task add "Urgent report" priority:H
     ```

2. **Recurring Tasks**:
   - Manage tasks that occur regularly.
     ```sh
     task add "Weekly team meeting" recur:weekly due:sunday
     ```

3. **Task Dependencies**:
   - Create tasks that depend on the completion of other tasks.
     ```sh
     task add "Start project phase 2" depends:1
     ```

4. **Custom Reports**:
   - Generate custom reports for specific needs.
     ```sh
     ```

5. **Bulk Modifications**:
   - Apply changes to multiple tasks at once.
     ```sh
     task +work modify project:NewProject
     ```

6. **Time Tracking**:
   - Track the time spent on specific tasks.
     ```sh
     task 2 start
     task 2 stop
     ```



7. Timesheet report

- For the current week
```sh 
task project:PERSONAL status:completed end.after:sow end.before:eow timesheet
```
- `end.after:soww: `This is a relative date filter. soww typically stands for
"start of work week." However, there seems to be a typo here. It should be sow
(start of week) instead. This filter selects tasks that were ended after the
beginning of the current week.

- `end.before:eow: ` This is another relative date filter, where eow stands for "end
of week." This filter selects tasks that were ended before the end of the
current week.

- If your week starts on a Monday and ends on a Sunday, end.after:sow will
filter for tasks completed after Monday 00:00, and end.before:eow will include
tasks completed before Sunday 23:59.

- For the week before:

```sh 
task project:HOT end.after:sow-1w end.before:sow timesheet
task project:PERSONAL status:completed end.after:sow-1 end.before:sow timesheet
```
- `end.after:sow-1w:` This filter selects tasks that ended after the start of
the week, one week ago (-1w is the modifier that moves one week back in time).

- `end.before:sow:`  This filter selects tasks that ended before the start of
the current week.


8. Search for tags when status:completed

```sh 
task project:WHOTS /TSG/ timesheet
```

