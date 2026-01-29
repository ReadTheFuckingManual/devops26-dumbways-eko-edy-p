# WEEK 1

## STAGE 1

### 1. step by step Akses server menggunakan kitty terminal

    1. buka VM ubuntu server dan login
    2. download Open SSH server di VM
```bash
sudo apt install openssh-server
```
    3. pastikan Status SSH di VM active(Running)
```bash
sudo systemctl status ssh
```
    4. chek IP VM dengan command 
```bash
ip a
```
![gambar](/task/week-1/day-3/asset/ip-a.png)
    5. buka kitty terminal
    6. akses VM dengan command di bawah (untuk ip nya menyesuaikan):
```bash
ssh eep@192.168.1.208
```
    7. masukkan password VM kalian, jika berhasil tampilannya akan seperti gambar di bawah    
![gambar](/task/week-1/day-3/asset/akses-vm.png)

---

### 2. Konfigurasi ssh agar bisa di akses hanya menggunakan publickey (password bisa dimatikan)

    1. generate SSH Key di Device kita
```bash
ssh-keygen
```
![gambar](/task/week-1/day-3/asset/ssh-keygen.png)
    2. masuk ke VM
    3. arahkan direktori ke `.ssh`
    4. masukkan ssh public key ke file `authorized_key`
```bash
echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIBu72xeCy3y+Wd7ODQM6RK3jpRy5tp2WaPfmLZkIIZ7C eep@eep.local" >> ~/.ssh/authorized_keys
```
![gambar](/task/week-1/day-3/asset/authorized_keys.png)
    5. test masuk VM menggunakan ssh public key dengan command di bawah (sesuaikan tempat penyimpanan ssh key nya)
```bash
ssh -i /Users/eep/Developments/playground/vm-ubuntu eep@192.168.1.208
```
![gambar](/task/week-1/day-3/asset/login-pubkey.png)
    6. sekarang atur config ssh agar bisa di akses hanya menggunakan publickey (password bisa dimatikan)
    7. masuk ke folder `/etc/ssh` edit file sshd_config seperti di bawah ini:
```bash
PubkeyAuthentication yes
PasswordAuthentication no
```
![gambar](/task/week-1/day-3/asset/edit-sshd-conf.png)
    8. restart SSH dengan command `sudo systemctl restart ssh`
    9. test login tanpa ssh public key, jika berhasil maka tampil seperti di bawah ini:
![gambar](/task/week-1/day-3/asset/login-without-pubkey.png)
    10. done, sekarang kita hanya bisa login ke VM menggunakan SSH Public Key


