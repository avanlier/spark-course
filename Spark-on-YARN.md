## Understanding the difference between YARN Client and Cluster  Modes

Objective: To test the consequences of making changes to container sizes, Maximum Application settings, and queue states; configure application preemption and create a set of queues and leaf queues which logically represent the organizations you support and their SLAs

1.  Open terminal
    
2.  Change to the ``~/spark3/examples/jars directory``.
    
	```
	cd spark3/examples/jars
	```
  
3.  Open a second terminal window.
    
4.  Once again, change to the ``~/spark3/examples/jars directory``.
	```
	cd ~/spark3/examples/jars
	``` 

5.  Position the two terminal windows so that both are visible on your screen side-by-side.
    
6.  Import ``sherlock.txt`` data into HDFS
    
	```
	hdfs dfs -mkdir data/  
	hdfs dfs -put ~/data/sherlock.txt data/
	```
  
7.  Type the Spark Submit command to execute wordcount in both terminal windows but do not press Enter to execute it.
    
**Terminal One**

```
spark3-submit --class org.apache.spark.examples.JavaWordCount --master yarn --deploy-mode client spark-examples_2.12-3.1.2.jar data/sherlock.txt
```
  

![](https://lh3.googleusercontent.com/F_gxLndvCyZ62o96vveWGEPl2l_5hUetNP6D9EOBzPQzctJIgsT41nSeh4xIITevH8PJF7HQ1SXuxltCPh0p9U2HXk3lEcKnoooT8xm_iKnDK9Pv4-SoAZX02w1sZq9ExDxoIv_4xQV7QvWiA5bxCA)

**List Application**

8.  While Application is running, open another terminal window and execute below command:
    
	```
	$ yarn application -list
	  ```

Output

![](https://lh6.googleusercontent.com/l3GUlNQUkfhlDJkT5Rc5magDoBPV80z8qRJ0HLcEtOWLyZOK89iS3nAcLDzD2fMeMxjonKytHDLBemjP8avaEYL9j9-Q9XiE5ap7xudHai7ca9GA80Jr-8GEHKfJW76gaRl-hEfEfq-6OjFH31JqgA)

To view Logs of the Application, execute below command:

![](https://lh3.googleusercontent.com/QllILmTFtc0oY6kXr4GUyET4LOO3_lF0c5xA00SYcLAwtSbgRy5U4MiSdLkrageAZ92p1yNEXpyzsfNlo750f-ShTXwjkAtsYalO321F4sHIwFaAVYJkemjz_889eYtKK6TXcPt3o2e5tSiiJdQfpg)

```
yarn logs -applicationId {your application  id}
```
  

![](https://lh5.googleusercontent.com/9yELsmS1RfsrvqEypNDSlzU9wMcb3wE9LYkkDsckGkbvDS8ja1lcd6oLQAX1jYto779FYRLbWH82zRS43BU-Hy7hGw5y_h3SELFMWgta2nbRDdf8rPYRKeGhsmWuVQWl48EuYHWRDoZxdjGVTkNT8g)

**Kill an Application**

9.  Below command kills a running application -
    

![](https://lh5.googleusercontent.com/tOrsMXvoXwwrljMFRIzrCy4Q0Yt6DQAGlEeOcBomA0vjVc1GSNDbvhKL9YynWzMFN3J-wbF_aJitrYpZDowmJZlgsfwHHddknZZwkywCngsnLz51xWmSycL2FYUp84JF7IKC6yQlzTS6pC-N_S7H0w)

```
yarn application -kill {your application  id}
```
  

**Exploring the YARN Cluster**

10.  Open the browser and connect to the CM at the URL http://localhost:7180
    
11.  Login to the CM UI using the username admin and the password admin
    
12.  Click Services in the CM UI.
    
13.  Select the YARN service on the Services page.
    

![](https://lh6.googleusercontent.com/VbqA0GxlqvdEW9ND1UB8aEJLPQJYdd21LKTGwGecjXBj_iRTOKaVWa9oT4hnuBsAefKlUCki1qevgbBCyJsHRay2tu3OD-JRDaU62UkRnu-LK2zpmSc4hg_YIC4NfxXLWfikeBdGdOzCV3Z8XdDK1Q)

14.  Click Web UI and select ResourceManager UI.
    

![](https://lh5.googleusercontent.com/zAICTxEYnoObAQt6oppxrrHXt4jQUaUra_rOZTdIUV2hu_sDtFVT7CWOYtU92rZiUsf7vxabyUNwnBCivbI1L8VBkYHrSYIvdSgOR4RDzxYkmELhW1EpJb60v1tW1oxufLYli9RHxd0d_xkHw8nDxQ)

The ResourceManager UI Web interface opens in another browser tab.

NOTE: If simply clicking the quick link fails to open the ResourceManager UI, replace the default URL in the browser tab with [datacouch.training.io:8088/cluster](http://datacouch.training.io:8088/cluster)

  
  

![](https://lh5.googleusercontent.com/dNtClNWyYM5EcRVqGhVpgbFukO5B49PwvVxIB1YJIAcnkl5CdpnqfkI1tPj9CutcEv0r7PxXQ-LLsCr1zMbGYG8pYi5kXCfZRogD7eYZmZ9u1HsaX3S9WZ14SJfKi15xpUczxGFvU-q9qTzpx0CBWw)

  

15.  This page will be refreshed in a moment once applications are running. Leave this tab open.
    

**Terminal Two**

```
spark3-submit --class org.apache.spark.examples.JavaWordCount --master yarn --deploy-mode cluster spark-examples_2.12-3.1.2.jar data/sherlock.txt
```

Open ResourceManager UI Web interface in another browser tab and click on application ID

![](https://lh4.googleusercontent.com/RTaX-yqzNbdn1t6v4uACgSiZZUqhuCktguFcL0mfHHvs3pxDXFtncsi19YwqHe3dZ8rsPF4i8e9hqSDBKaaHRtoV0ek6X-C_L9pkcQDJJIjBy_Rg7DSMB_58fsMymYw7RECHheeRBwCfkBrv-bPuIQ)  

![](https://lh6.googleusercontent.com/mYJuKKAFbUEi8wTvo02NIQywW6uxiQO3Y8qnDPYFT282IFjiP1oImfvyK2VGWf1KLfUHB-hbtAM6pI0Dphp6N4tl2DPfxe0TxbcEazxO_-8y6Xkx4iOn5BO76gc06JuV6CeyCaG7a9-Wa8FWmqrM4A)

![](https://lh6.googleusercontent.com/Iwe542zGyiOlUn9sIvPS2Kto_74W8s20Z7MNFWb7c2tCl4tjYbPiNpgl9mcQCaTWDeu4t9R7kyJQcLzgTpDuQrC5xwHtGUfkwuKIqGIEHM520YxnM-Wgmk5EQPlN6cbNJ8KGNkZeJYEj9OE-VruMOQ)
