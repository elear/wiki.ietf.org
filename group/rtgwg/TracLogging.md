---
title: Trac Logging
description: 
published: true
date: 2022-12-23T20:01:42.027Z
tags: 
editor: markdown
dateCreated: 2022-12-23T20:01:37.962Z
---

# Trac Logging

Trac supports logging of system messages using the standard [logging module](http://docs.python.org/library/logging.html) that comes with Python.

Logging is configured in the `[logging]` section in [trac.ini](/group/rtgwg/TracIni).

## Supported Logging Methods
The log method is set using the `log_type` option in [trac.ini](/group/rtgwg/TracIni), which takes any of the following values:

**none**
	Suppress all log messages.
**file**
	Log messages to a file, specified with the `log_file` option in [trac.ini](/group/rtgwg/TracIni). Relative paths in `log_file` are resolved relative to the `log` directory of the environment.
**stderr**
	Output all log entries to console ([tracd](group/rtgwg/TracStandalone) only).
**syslog**
	(UNIX) Send all log messages to the local syslogd via named pipe `/dev/log`. By default, syslog will write them to the file /var/log/messages.
**eventlog**
	(Windows) Use the system's NT Event Log for Trac logging.

## Log Levels
The verbosity level of logged messages can be set using the `log_level` option in [trac.ini](/group/rtgwg/TracIni). The log level defines the minimum level of urgency required for a message to be logged, and those levels are:

**CRITICAL**
	Log only the most critical (typically fatal) errors.
**ERROR**
	Log failures, bugs and errors.
**WARN**
	Log warnings, non-interrupting events.
**INFO**
	Diagnostic information, log information about all processing.
**DEBUG**
	Trace messages, profiling, etc.

Additionally, you can enable logging of SQL statements at debug level. This is turned off by default, as it's very verbose. Set `[trac] debug_sql = yes` in [TracIni](/group/rtgwg/TracIni) to activate.

## Log Format
The output format for log entries can be specified through the `log_format` option in [trac.ini](/group/rtgwg/TracIni). The format is a string which can contain any of the [Python logging Formatter variables](http://docs.python.org/library/logging.html#logrecord-attributes). Additonally, the following Trac-specific variables can be used:

**$ (basename)s**
	The last path component of the current environment.
**$ (path)s**
	The absolute path for the current environment.
**$ (project)s**
	The originating project's name.

Note that variables are identified using a dollar sign (`$(...)s`) instead of percent sign (`%(...)s`).

The default format is:

`log_format = Trac[$(module)s] $(levelname)s: $(message)s`

In a multi-project environment where all logs are sent to the same place (e.g.` syslog`), it makes sense to add the project name. In this example we use `basename` since that can generally be used to identify a project:

`log_format = Trac[$(basename)s:$(module)s] $(levelname)s: $(message)s`

---
See also: [TracIni](/group/rtgwg/TracIni), [TracGuide](/group/rtgwg/TracGuide), [TracEnvironment](/group/rtgwg/TracEnvironment)
&nbsp;
&nbsp;
&nbsp;

---

*The content of this page was last updated on 2016-05-11. It was migrated from the old Trac wiki on 2022-12-23.*