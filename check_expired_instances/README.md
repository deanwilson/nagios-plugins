# check_expired_instances #

A Nagios check that reports all the AWS instances in a
given region that have been running for longer than the specified
number of days.

## Dependencies

 * Python dateutil module
 -packaged as python-dateutil on Debian and fedora
 * boto module

## Configuration

There should be a configuration file containing either default access
credentials to be used for every region or a specific ini-file stanza for
specific regions with different access requirements

    $ cat check_expired_instances.conf.sample
    [default]
    # use these credentials by default
    aws_access_key_id     = AAAAAAAA
    aws_secret_access_key = AAAAAAAAAAAAAAAA

    [us-east-1]
    # override the creds for this region
    aws_access_key_id     = BBBBBBBB
    aws_secret_access_key = BBBBBBBBBBBBBBBB

You can have multiple stanzas each representing a single region in the same
config file.

In addition to the config file you can also use the command line switches
or the AWS_ACCESS_KEY, AWS_SECRET_KEY and REGION environment variables
to override the values in the config file.

## Usage

    # basic Nagios check
    $ check_expired_instances.py --config-file us-east-1.aws.ini --region us-east-1 --warning 30 --critical 30

    check_expired_instances.py: CRIT 41 instances are past their expiry date in us-east-1


    # and to generate a list of failing ids for piping to another command
    $ check_expired_instances.py --config-file us-east-1.aws.ini --region us-east-1 \
      --warning 30 --critical 30 --crit-ids

    i-424f19ec
    i-242ebf41
    i-424439fa

You can run a single sweep of all regions by specifying `--region all` on
the command line.
