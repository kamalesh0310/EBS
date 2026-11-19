##WORKING WITH EBS

Aim
To create and configure an Amazon Elastic Block Store (EBS) volume, attach and mount it to an Amazon EC2 instance, create a snapshot backup, and restore the snapshot to a new EBS volume.

Algorithm / Steps
Create a new Amazon EBS volume with a size of 1 GiB.

Select the same Availability Zone as the EC2 instance.

Attach the EBS volume to the EC2 instance using /dev/sdb.

Connect to the EC2 instance using AWS Systems Manager Session Manager.

Check the available storage using df -h.

Create an ext3 file system on the EBS volume.

Create the /mnt/data-store directory.

Mount the EBS volume to /mnt/data-store.

Configure /etc/fstab for automatic mounting.

Verify that the EBS volume is successfully mounted.

Create file.txt inside the mounted EBS volume.

Verify the contents of the created file.

Create an EBS snapshot named My Snapshot.

Delete file.txt from the original EBS volume.

Create a new EBS volume from the snapshot.

Attach the restored volume to the EC2 instance using /dev/sdc.

Create the /mnt/data-store2 directory.

Mount the restored volume to /mnt/data-store2.

Verify that file.txt has been successfully restored.

Program
1. Check Available Storage
df -h
2. Create an ext3 File System
sudo mkfs -t ext3 /dev/sdb
3. Create a Mount Directory
sudo mkdir /mnt/data-store
4. Mount the EBS Volume
sudo mount /dev/sdb /mnt/data-store
5. Configure Automatic Mounting
echo "/dev/sdb   /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
6. View the File System Configuration
cat /etc/fstab
7. Verify the Mounted Volume
df -h
8. Create a File in the EBS Volume
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
9. Read the File
cat /mnt/data-store/file.txt
10. Delete the File
sudo rm /mnt/data-store/file.txt
11. Verify File Deletion
ls /mnt/data-store/
12. Create a Mount Directory for the Restored Volume
sudo mkdir /mnt/data-store2
13. Mount the Restored EBS Volume
sudo mount /dev/sdc /mnt/data-store2
14. Verify Snapshot Restoration
ls /mnt/data-store2/
Expected output:
file.txt
Snapshot:
<img width="1920" height="1080" alt="Screenshot (79)" src="https://github.com/user-attachments/assets/316a2906-954b-4462-b660-da319b06fb8c" />
<img width="1920" height="1080" alt="Screenshot (81)" src="https://github.com/user-attachments/assets/705f9fc5-32f1-42fa-b04f-08891a5ffe23" />
<img width="1920" height="1080" alt="Screenshot (83)" src="https://github.com/user-attachments/assets/2ad3d555-feac-424f-94bb-f2633fccd6f4" />
<img width="1920" height="1080" alt="Screenshot (84)" src="https://github.com/user-attachments/assets/aee190f8-c194-47c3-8ac7-0f96aa785a63" />
<img width="1920" height="1080" alt="Screenshot (85)" src="https://github.com/user-attachments/assets/22972aa4-a563-4cae-ba6a-4b0174e0532d" />
<img width="1920" height="1080" alt="Screenshot (88)" src="https://github.com/user-attachments/assets/51b615cc-0307-4b08-8de2-0c614c4d3de9" />
<img width="1920" height="1080" alt="Screenshot (89)" src="https://github.com/user-attachments/assets/7e68d318-7825-4dfa-9bb1-a38b3e08f710" />
<img width="1920" height="1080" alt="Screenshot (90)" src="https://github.com/user-attachments/assets/f877e34f-a851-4606-b841-db202590a977" />

Result
Thus, an Amazon EBS volume was successfully created, attached and mounted to an EC2 instance. A snapshot backup was created and restored to a new EBS volume.
