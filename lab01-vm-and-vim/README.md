# Lab 1: VM setup and VIM basics

## Goal

Get the course virtual machine running and learn basic VIM navigation and editing.

## Tools and concepts

- Oracle VirtualBox: importing an `.ova` appliance, snapshots, VM settings
- 32-bit Ubuntu 18.04 guest (course image)
- VIM: `hjkl` movement, `vimtutor`, the vimgenius online quizzes
- NetHack (`xnethack`), used only as `hjkl` practice

## What I did

- Imported the course appliance into VirtualBox and took an initial snapshot to roll back to.
- Timed the boot and tried the optional tuning steps one at a time: VT-x (already on in my BIOS), Guest Additions, more CPU cores, 2D/3D graphics acceleration with more video memory.
- Played five NetHack rounds using only `hjkl` to move.
- Finished `vimtutor` lessons 1 and 2 and the first two vimgenius quizzes.

## Result

- First boot took about 10 seconds. My worksheet lists 4 cores, 4 GB RAM, a 30 GB disk and an SSD.
- The tuning steps did not help on my hardware. Boot times I measured after each step were 20 to 40 seconds, and 30 seconds with all of them applied, so the untuned VM was the fastest.
- No step froze the system.

The report was graded from screenshots, which are not in this repository.
