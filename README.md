# check_haproxy_stats
check_haproxy_stats is a Nagios check for Haproxy using the statistics page

## prerequisites

This script uses theses libs : File::Basename LWP::UserAgent URI::URL HTTP::Request IO::Socket::SSL IO::Socket::UNIX MIME::Base64 Readonly Monitoring::Plugin Data::Dumper

to install them type :
```shell
sudo cpan File::Basename LWP::UserAgent URI::URL HTTP::Request IO::Socket::SSL IO::Socket::UNIX MIME::Base64 Readonly Monitoring::Plugin Data::Dumper
```
## Use case 
```bash
check_haproxy_stats.pl 1.1.5

This program is free software; you can redistribute it and/or modify it
under the same terms as Perl 5.10.1
For more details, see http://dev.perl.org/licenses/artistic.html

This program is distributed in the hope that it will be
useful, but without any warranty; without even the implied
warranty of merchantability or fitness for a particular purpose.

check_haproxy_stats.pl is a Nagios check for Haproxy using the statistics page via local socket or https

Usage: check_haproxy_stats.pl [-U <URL> -u <User> -P <password>]  [-p <proxy>] [-x <proxy>] [-m] [-n] [-s <servers>] [-i <REGEX>] [-w <threshold> ] [-c <threshold> ]  [-t <timeout>]

 -?, --usage
   Print usage information
 -h, --help
   Print detailed help screen
 -V, --version
   Print version information
 --extra-opts=[section][@file]
   Read options from an ini file. See https://www.monitoring-plugins.org/doc/extra-opts.html
   for usage and examples.
 -U, --url=STRING
  Use HTTPS Statistics URL instead of socket the url is used like this https://$url;csv
 -S, --socket=STRING
  Use named UNIX socket instead of default (/var/run/haproxy.sock)
 -m, --ignoremaint
 Assume servers in MAINT state to be ok.
 -n, --ignoredrain
  Assume servers in DRAIN state to be ok.
 -i, --ignoreregex=STRING
  Ignore servers that match the given regex.
 -p, --proxy=STRING
  Check only named proxies, not every one. Use comma to separate proxies in list.
 -P, --noproxy=STRING
  Do not check named proxies. Use comma to separate proxies in list.
 -u, --user=STRING
  User name  for the HTTPS URL
 -P, --Password=STRING
  User password for the HTTPS URL
 -w, --warning=threshold
   See https://www.monitoring-plugins.org/doc/guidelines.html#THRESHOLDFORMAT for the threshold format.
 -c, --critical=threshold
   See https://www.monitoring-plugins.org/doc/guidelines.html#THRESHOLDFORMAT for the threshold format.
 -r, --raw
   Just dump haproxy stats and exit
 -s, --slave
   Check if the named serveur have no connexion Use comma to separate serveur in list .
 -t, --timeout=INTEGER
   Seconds before plugin times out (default: 30)
 -v, --verbose
   Show details for command-line debugging (can repeat up to 3 times)

```

sample :

```shell
# NRPE
sudo ./check_haproxy_stats.pl -w 60 -c 80 -S /var/run/haproxy/admin.sock -p front_mpe

# On monitoring poller 
./check_haproxy_stats.pl --url MyUrl --user supervision --Password mdp -p front_mpe
```

Exemples de retour :
```shell
Check haproxy OK - checked proxies: front_mpe|front_mpe-FRONTEND=1034;2400;3200;0;4000




