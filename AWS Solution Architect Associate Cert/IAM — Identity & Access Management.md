![[Screenshot 2026-02-19 at 7.21.55 PM.png]]
> [!info] Key Facts
> - **Global Service** — not region-specific
> - Root account is created by default — use it as little as possible
> - Users = people in your org | Groups = collections of users (groups can't contain groups)

---

## Permissions

Users or Groups are assigned **policies** — JSON documents that define what they can do.

> [!example] Sample Policy
> ```json
> {
>   "Version": "2012-10-17",
>   "Statement": [
>     {
>       "Effect": "Allow",
>       "Action": "ec2:Describe*",
>       "Resource": "*"
>     }
>   ]
> }
> ```

> [!tip] Golden Rule
> AWS follows the **principle of least privilege** — only give users the permissions they actually need.

---

## Key Concepts

| Concept         | Notes                                                      |
| --------------- | ---------------------------------------------------------- |
| **Access Keys** | Used for CLI/API access. User-level — never share them     |
| **AWS CLI**     | Command line tool to manage AWS resources                  |
| **AWS SDK**     | Libraries for accessing AWS via code (e.g. Python = boto3) |
| **CloudShell**  | Browser-based terminal — only available in certain regions |

<br><br>

<span style="float:left">← [[Getting Started]]</span><span style="float:right">[[Application Load Balancer (ALB)]] →</span>
