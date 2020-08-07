# Logging into ECR with Docker and AWS CLI v2

	aws ecr get-login-password | docker login --username AWS --password-stdin <url>

URL will be something like:

	<account_id>.dkr.ecr.<region>.amazonaws.com
