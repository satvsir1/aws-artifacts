# EBS
## Creation, attachment and detachment of volume

First of all, we need to create an ec2 instance.
Thus, we need to go to EC2 console
![](../images/ec2-console.jpg)

1. Instance creation
- Navigate to EC2 > Instances > Instances
![](../images/ec2-instances.jpg)
- Click "Launch instances" button
![](../images/ec2-launch-instances.jpg)
- Select Amazon Linux 2 AMI
![](../images/ec2-amzn-linux-ami.jpg)
- Choose free tier eligible type of instance
![](../images/ec2-free-tier-type.jpg)
- Click "Review and launch" button
- Click "Launch" button
- Choose "Create new keypair" and give it a name
![](../images/ec2-keypair.jpg)
- Click "Download Key Pair" button, and save the file to your work directory
- Click "Launch instances" button
- Click "View Instances" button and check instance details for availability zone, where your instance is running. Save it anywhere.
2. Volume creation
- Return to EC2 console
- Navigate to EC2 > Elastic Block Store > Volumes
![](../images/ec2-volumes.jpg)
- Click "Create Volume" button
![](../images/ec2-create-volume.jpg)
- In "Volume Type" drop-down menu choose "General Purpose SSD (gp2)"
- In "Size" type 10
- In "Availability Zone" drop-down menu choose the availability zone your instance is running in
- Click "Add tag" button and add tag with key "Name" and value "test volume"
![](../images/ec2-create-volume2.jpg)
- Click "Create Volume" button
- Click "Close" button
3. Volume attachment
- Navigate to EC2 > Elastic Block Store > Volumes
- Choose our new "Test Volume" volume
![](../images/ec2-test-volume.jpg)
- Click "Actions" button and choose attach volume
![](../images/ec2-attach-volume.jpg)
- Choose instance ID and device ID for volume mapping
![](../images/ec2-attach-volume2.jpg)
- Click "Attach button"
- Wait until volume state is "in-use"
4. Volume mount and filesystem setup
- Navigate to EC2 > Instances > Instances
- Click on your instance ID
- Click "Connect" button
![](../images/ec2-connect.jpg)
- Choose "SSh Client" and go through the instructions
![](../images/ec2-connect-ssh.jpg)
- Connect to the instance
- Check if the operating system sees your volume as block device
![](../images/ec2-lsblk.jpg)
- Create new partition or format the whole disk
![](../images/ec2-mkfs.jpg)
- Mount the formatted volume to the desired mount point
`sudo mount /dev/nvme1n1 /mnt/`
- Create text file and insert some text in it
`echo 'Hello from instance 1' > test.txt`
-  Copy the file to the volume
`sudo cp test.txt /mnt/`
-  Unmount volume
`sudo umount /mnt/`
5. Volume detachment
- Return to EC2 console
- Navigate to EC2 > Elastic Block Store > Volumes
- Choose our new "Test Volume" volume
- Click "Actions" button and choose detach volume 
- Wait until volume state is "available"
6. Instance termination
- Navigate to EC2 > Instances > Instances
- Choose your instance ID
- Click "Instance State" button
- Choose "Terminate Instance"
- Click "Terminate" button
7. Creation of new instance and volume attachment
- Create new instance in the same availability zone
- After instance creation attach volume to the instance and mount it to the mount point
> Please note, you do not need to reformat the volume. Just mount it.
- Ensure the file from instance 1 still exists on the volume and the data persists
`sudo ls /mnt`
`sudo cat /mnt/test.txt`
8. Clean-up procedures
- Detach the volume
- Terminate instance
- Navigate to EC2 > Elastic Block Store > Volumes
- Choose our new "Test Volume" volume
- Click "Actions" button and choose delete volume 
- Click "Yes, delete" button

