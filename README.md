# jdrivesync

Command-line tool for synchronizing local folders with Google Drive.

## What it does

- syncs local files to Google Drive and back
- supports integration tests with a separate account
- builds with Maven

## Architecture

The CLI builds a synchronization plan from the local directory and Google Drive listings. Local filesystem and Drive API operations are handled through separate paths, while the planner decides which files need upload, download or no action.

## Links

- DeepWiki: https://deepwiki.com/eneekoruiz/jdrivesync
