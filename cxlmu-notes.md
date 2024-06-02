## Notes

#### Building qemu
Make sure on `cxlmu` branch

```
mkdir build
cd build
../configure --enable-debug --prefix=/usr/local --enable-slirp
make -j
sudo make install
```

#### Testing

```
wget -O ~/ubuntu.img https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64.img
./qemu-img create -f qcow2 -F qcow2 -b ~/ubuntu.img ~/root.qcow2 10G
virt-customize -a ~/root.qcow2 --root-password password:root
```

```
sudo ./qemu-system-x86_64 -m 20g -enable-kvm -drive file=/home/midhul/root.qcow2,driver=qcow2 -net nic -net user,hostfwd=tcp::10022-:22 -nographic
```

Let it boot, and then you can login with username/password root/root, and you will have a shell.
