# Email


## Sending Email

```ruby
#!/usr/bin/env ruby
# 
#
require 'net/smtp'

def send_mail(smtpsrv, username, password, frmemail, dstemail)

  msg  = "From: #{frmemail}\n"
  msg += "To: #{dstemail}\n"
  msg += "Date: #{date}\n"
  msg += "Subject: Email Subject\n"
  msg += "Content-type: text/html\n\n"
  msg += "<strong>Hi<br>Please click to win!</strong>"

  begin

    Net::SMTP.start(smtpsrv, 25, 'localhost', username, password, :login) do |smtp|
      smtp.send_message msg, frmemail, dstemail
    end
    puts "[+] Email has been sent successfully!"
  rescue Exception => e
    puts "[!] Failed to send the mail"
    puts e
  end

end

smtpsrv  = ARGV[0]
username = "admin@offsec.local"
password = "123456"
frmemail = "admin@offsec.local"
dstemail = "admin@offsec.local"

smtpsrv = ARGV[0]
if smtpsrv.nil?
  puts "[!] IP address Missing \nruby #{__FILE__}.rb [IP ADDRESS]\n\n"
  exit 0
end

send_mail smtpsrv, username, password, frmemail, dstemail
```