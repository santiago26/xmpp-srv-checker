xmpp-srv-checker
================

xmpp.net verification

When a server administrator registers a public XMPP service with xmpp.net, here is how we verify the registration:

Ensure that the request is approved by one of the official representatives for the root domain by forwarding the message sent on the operators@xmpp.org list to (1) the email address(es) listed in the whois record for the root domain and (2) the hostmaster/postmaster/webmaster email addresses for the root domain. (By “root domain” we mean the lowest-level domain that can be looked up in whois — e.g., if the XMPP service is running at im.example.com then we contact the owners and admins for example.com.)

Typically the message we send says something like this:

“Please verify that you approve of this request to add im.example.com to the list at http://xmpp.net/…”

Check for appropriate DNS SRV records using the dig command, such as:

dig +short -t SRV _xmpp-client._tcp.im.example.com

dig +short -t SRV _xmpp-server._tcp.im.example.com

Verify that there is indeed an XMPP service running at the domain for server-to-server and client-to-server communications using telnet to the ports discovered via SRV lookups, such as:

telnet im.example.com 5222

telnet im.example.com 5269

Validate the certificate against the root cert of the security provider to make sure that secure connections can be established without errors. We do this by checking STARTTLS on port 5222 or SSL on port 5223 using the OpenSSL s_client feature, such as:

openssl s_client -connect im.example.com:5222 -starttls xmpp -CAfile startcom.crt

openssl s_client -connect im.example.com:5223 -CAfile startcom.crt

Visit the website of the service to make sure that it is accurate, provides contact information, etc.

Communicate with the service administrator via XMPP.
