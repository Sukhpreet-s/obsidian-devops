Better solution for scripting tedious management tasks.
Uses declarative programming approach. Specify what exactly needs to be done. Chef figures out how to get it done.

Uses pull based model - Client servers connect to the main server to get the required configuration.

Idempotency:
- Example: user creation -> user is only created if it doesn't exist. If already exists, the task is skipped.
Convergence:
- In a multi-step task -> Check if each of the task is already done. If already done, skip it, else do it.

Advantages:
- No complex scripting
- Consistent in Heterogenous environments
- Declarative pattern
- Idempotent