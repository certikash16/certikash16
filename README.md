#import required modules/packages/library
import pexpect
#define variables
ip_address = '192.168.56.101'
username = 'prne'
password = 'cisco123!'
password_enable = 'class123!'

# Create the SSH session
session = pexpect.spawn ('ssh ' + username + '@' + ip_address,
                         encoding ='utf-8',timeout=20)
result = session.expect(['password:', pexpect.TIMEOUT, pexpect.EOF])
# check for error, if exists then display error and exit 
if result != 0:
    print('---FAILURE! creating session for:',ip_address)
    exit()
   
    # session expecting password, enter details
    session.sendline (password)
    result=session.expect(['>', pexpect.TIMEOUT, pexpect.EOF])

    #check for error, if exists then display error and exit
    if result != 0:
        print('---FAILURE! entering password: ',password)
        exit()

#enter enable mode
session.sendline('enable')
# display a success message if works
print('-------------------------------------------------------')
print('')
print('--- success! connecting to: ', ip_address)
print('---               username: ', username)
print('---               password: ', password)
print('')
print('-------------------------------------------------------')
# terminate SSH session
session.close()





