# This is how we can create a normal user account</br>

### Create a normal user of wheel group</br>
-> **useradd --create-home *USER_NAME***</br>
E.g.: -> useradd --create-home me</br>
-> **passwd *USER_NAME***</br>
E.g.: -> passwd me</br>
-> **usermod --append --groups wheel *USER_NAME***</br>
E.g.: -> usermod --append --groups wheel me</br>

### Add sudo group and add the user to it</br>
-> **groupadd sudo**</br>
-> **usermod --append --groups sudo USER_NAME**

### Add SUDO permissions to the user</br>
-> **EDITOR=nano visudo**</br>
Notes: we need to uncomment: **%wheel ALL=(ALL) ALL** and **%sudo ALL=(ALL) ALL**</br>

### Allow sudo to be called by users</br>
-> **chmod 4755 /usr/bin/sudo**</br>
