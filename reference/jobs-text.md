## Jobs

### Schedule
* **&nbsp;0 0 * * *&nbsp;** cron schedule: See [crontab.guru](https://crontab.guru/)
* **60** period in seconds
* **0** disables a job.

| Job                                | Description                              | Default Schedule    |
| ---------------------------------- | ---------------------------------------- | ----------- |
| tenant.storage.report              | Updates the tenant table with storage in MB | 0 3 * * *   |
| tenant.users.report                | Updates the tenant table with userCount  | 0 2 * * *   |
| storage.garbage.collector.interval | Deletes files from the filesystem that are marked for deletion | 0 3 * * *   |
| db.backup.schedule                 |                                          | 0           |
| file.cleanup.schedule              | Cleanup temp file directory              | 0 * * * *   |
| health.report.schedule             |                                          | 0           |
| group.sync.interval                |                                          | 0           |
| scheduled.notification.interval    | Trigger diarize,                         | 1800        |
| sync.interval                      | Import and sync, sync from table to pt   | */5 * * * * |
| message.retry.check.interval       | Retry period for failed messages         | 60          |
| workflow.timeout.check.interval    | Period to check for workflow tasks that have timed out | 900         |
| index.backup.schedule              |                                          | 0           |
| out.of.office.job                  |                                          | 600         |

