# Presentation Script: Kyeongjun Yu (Intro and Claude Code)

Hi, we are Kyeongjun, Ryan, and ByeongHak. Today we look at AI coding agents that went wrong.

Claude Code runs commands and edits files inside a sandbox. Three confirmed advisories show the sandbox had serious bugs. All three are rated High on the CVSS scale, which scores bugs from 0 to 10.

In one bug, the sandbox did not protect a hook config file that did not exist yet. The agent created it, and its hook ran on the next startup.

In another, a symlink, which is a shortcut, let the agent write files outside the project folder.

Users also reported real data loss. One user said a cleanup script walked into Windows junctions and deleted 48,218 project files in 103 seconds.

The sandbox protected what existed, but not what could be created, or reached through shortcuts. Next, we will show the OpenAI case.
