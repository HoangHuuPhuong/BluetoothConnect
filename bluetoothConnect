#!/usr/bin/python
from bluetooth import *
import sys

class cl_connect(object):
    "This is for connect ubuntu with android smartphone"
    def __init__(self):
        self.addr = "08:37:3D:7D:9D:D7"
        self.uuid = "8ce255c0-200a-11e0-ac64-0800200c9a66"
        self.server_sock = BluetoothSocket(RFCOMM)
        self.server_sock.bind(("",PORT_ANY))
        self.server_sock.listen(1)

        port = self.server_sock.getsockname()[1]

        advertise_service( self.server_sock, "SampleServer",
                   service_id = self.uuid,
                   service_classes = [ self.uuid, SERIAL_PORT_CLASS ],
                   profiles = [ SERIAL_PORT_PROFILE ], 
#                   protocols = [ OBEX_UUID ] 
                    )

        #print "Waiting for connection on RFCOMM channel %d" % port
        self.client_sock, self.client_info = self.server_sock.accept()
        #print "Accepted connection from ", client_info

    def f_receiveSignal(self):
        "Receive signal from Android smartphone"
        try:
            while True:
                data = self.client_sock.recv(1024)
                if len(data) == 0: break
                #print "received [%s]" % data
                if data == "SCREEN ON":
                    screenStatus = True ## ON
        except IOError:
            pass

        print "disconnected"
        self.client_sock.close()
        self.server_sock.close()
        print "all done"

def main():
    connect = cl_connect()
    connect.f_receiveSignal()
if __name__ == '__main__':
    main()
