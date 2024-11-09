
Using START_REDELIVER_INTENT instead of START_STICKY can be a good improvement for your AlarmService. Here’s why:

Difference Between START_STICKY and START_REDELIVER_INTENT
START_STICKY:

The service is restarted if it gets terminated by the system.
However, the Intent that was passed to onStartCommand() might be null when the service restarts. This is why you encountered a NullPointerException.
START_REDELIVER_INTENT:

The service is restarted if it gets terminated by the system.
The last delivered Intent is re-sent when the service restarts. This means the intent parameter will not be null after a restart.
This is a safer option when your service relies on the data in the Intent.
When to Use START_REDELIVER_INTENT
You should use START_REDELIVER_INTENT if:

Your service requires the Intent data to function correctly (which is true in your case since you rely on alarmUid and other extras).
You want to ensure that the service always receives the last Intent, even if the system restarts it.