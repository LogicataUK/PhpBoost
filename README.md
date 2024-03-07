[![Logicata](doc/images/header.png)](https://www.logicata.com/)

# PhpBoost

PhpBoost is a small tool which helps to work out the best PHP-FPM parameters for a single EC2 host (or a pool of hosts inside an auto-scaling target group), as described in the Logicata article [*AWS best practices for PHP*](https://www.logicata.com/blog/aws-best-practices-for-php).

The tools collect some system metrics to suggest an optimised PHP-FPM configuration, like in the following demo:

![PhpBoost Demo](doc/images/phpboost/phpboost-demo.gif)

## Installation

Copy and paste the following commands in your terminal:

```bash
mkdir -p /opt/logicata/phpboost && \
  curl "https://raw.githubusercontent.com/LogicataUK/blog-supporting-tools/master/src/2022/aws-best-practices-for-php/phpboost" -s -o /opt/logicata/phpboost/phpboost && \
  chmod +x /opt/logicata/phpboost/phpboost && \
  ln -s /opt/logicata/phpboost/phpboost /usr/bin/phpboost
```



## How to use the tool

Please note that the tool assumes the EC2 hosts are only running the PHP application and everything else (database, in-memory cache) is offloaded to AWS services like RDS or ElastiCache.

To use the tool:

- Define the time you want to analyse your system (in seconds).
- Launch *phpboost*.
- Stress your system by trying to create a usage scenario as realistic as possible.
- Wait for the analysis to end and get the suggested PHP-FPM configuration.



## Examples

Collect metrics for 30 minutes (1800 seconds) on an EC2 instance member of an [auto-scaling group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/auto-scaling-groups.html):

```bash
phpboost --time 1800 --autoscale
```

Collect metrics for 10 minutes (600 seconds) on a single EC2 instance:

```bash
phpboost --time 600
```



## Command synopsis

```
Usage:
  ./phpboost [-t|--time time] [-a|--autoscale]

Options:
  -t, --time         The approximate amount of seconds the script
                     should run to collect system usage metrics
                     (default 2s)
  -a, --autoscale    Add this parameter if you have AWS autoscaling
                     configured (You should contact us if you
                     haven't :)
  -h, --help         Shows this help.

Examples:

  Collect data metrics for 3600 seconds (1 hour)
  ./phpboost -t 3600                      
```

---

<!--suppress HtmlDeprecatedAttribute -->
<div align="center">
  <a href="https://www.logicata.com" target="_blank">© 2022-2024 - Logicata Ltd</a>
</div>


