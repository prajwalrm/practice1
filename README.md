from qz.core.spongebob import Job, init
from datetime import datetime, timedelta

# Initialize SpongeBob framework
init(sourcePath="/path/to/jobs", dryRun=False, maxJobs=10, host="localhost")

# Define batch dates (10 days in the past)
start_date = datetime.today() - timedelta(days=10)
batch_dates = [(start_date + timedelta(days=i)).strftime("%Y-%m-%d") for i in range(10)]

# Create jobs for each batch date
jobs = []
for batch_date in batch_dates:
    job = Job(
        name=f"NextDayUTI_{batch_date}",
        command=f"python /path/to/nextday_uti_determination.py {batch_date}",
        enabled=True
    )
    jobs.append(job)

# Execute jobs
for job in jobs:
    job.run()
