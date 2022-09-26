## Configure Router-on-a-Stick Inter-VLAN Routing
#### Topologie
![image](https://user-images.githubusercontent.com/99610266/192247299-86b376da-9c4a-481c-a896-04bae4a79568.png)
### Part 1. Build the Network and Configure Basic Device Settings
##### I configured basic settings for each devices.
### Part 2: Create VLANs and Assign Switch Ports
##### Next, I created VLANs and assigned to appropriate interfaces.
![image](https://user-images.githubusercontent.com/99610266/192249143-9b8bf587-e588-4ce0-8ee1-d42fd372e3e0.png)
### Part 3: Configure an 802.1Q Trunk Between the Switches
#### I configured trunks interfaces between switches and changed a native vlan. 
![image](https://user-images.githubusercontent.com/99610266/192252912-41ac9a1e-0e2c-43df-ac6f-db9e95b3016e.png)
![image](https://user-images.githubusercontent.com/99610266/192250125-27fae392-05ee-407b-9c9a-c7ca6b6a2074.png)
### Part 4: Configure Inter-VLAN Routing on the Router
#### 1. I actived an interfece e0/0 on a router R1.
#### 2. I configured subinterfaces for each VLAN and assigned IP-address for them.
![image](https://user-images.githubusercontent.com/99610266/192252097-77e31ef2-ca65-4a3f-a86c-80a4b696b94d.png)
### Part 5: Verify Inter-VLAN Routing is Working
#### All tests completed successful.
![image](https://user-images.githubusercontent.com/99610266/192252613-708d4deb-e326-4508-bfd9-52de7fbd9c7b.png)

