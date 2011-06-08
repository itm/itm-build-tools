ITM Build Tools
===============

ITM Build Tools shall help to ease and harmonize e.g. the coding style in our ITM projects.

Checkstyle
----------

We use [Checkstyle][checkstyle] to enforce certain coding style guidlines. Checkstyle can be executed with Maven.

Usage
-----

In your POM add the following sections:

    <project>
      <build>
    	[...]
    	<pluginManagement>
    		  <plugins>     
    		       [...]
                   <plugin>
                       <groupId>org.apache.maven.plugins</groupId>
                       <artifactId>maven-checkstyle-plugin</artifactId>
                       <version>2.6</version>
                       <dependencies>
                           <dependency>
                               <groupId>de.uniluebeck.itm</groupId>
                               <artifactId>itm-build-tools</artifactId>
                               <version>1.0</version>
                           </dependency>
                       </dependencies>
                       <configuration>
                           <configLocation>itm_checks.xml</configLocation>
    			           <enableRulesSummary>false</enableRulesSummary>
                       </configuration>
                   </plugin>
               </plugins>    
    	</pluginManagement>
       </build>
       [...]
       <reporting>
           <plugins>
               <plugin>
                   <groupId>org.apache.maven.plugins</groupId>
                   <artifactId>maven-checkstyle-plugin</artifactId>
                   <version>2.6</version>
               </plugin>
           </plugins>
       </reporting>
       [...]
       <pluginRepositories>
	       <pluginRepository>
			   <id>itm-maven-repository-releases</id>
			   <url>http://www.itm.uni-luebeck.de/projects/maven/releases/</url>
		   </pluginRepository>		   
	   </pluginRepositories>
    </project>

Generate a report on the command line:

    $ mvn checkstyle:checkstyle site

This generates a checkstyle reportand a HTML page. Using the target `site` we assure, that all css-Files, etc. are avaiable. The html page(s) is(are) located at `${module}/target/site/checkstyle.html`. 

If you are only interested in the plain report, you can leave out the `site` target.

More info can be found at: [Checkstyle Project][checkstyle] and [Maven Checkstyle Plugin][maven-checkstyle-plugin].

What if my code exceeds the 120 character line limit?
-----------------------------------------------------

Here are some examples how this situation can be handled:

Example 1: Conditions in if-statments

     if (authenticationManager.getSecretAuthenticationKeys() != null
             && !authenticationManager.getSecretAuthenticationKeys().isEmpty()) {
         ...
     }

Example 2: Long method signatures

     public List<SecretReservationKey> makeReservation(final String rsEndpointUrl,
                                                       final List<SecretAuthenticationKey> secretAuthenticationKeys,
                                                       final ConfidentialReservationData confidentialReservationData)
     throws AuthenticationException, ReservationException {
        ...
     }
     

Example 3: Constructors with many arguments

     public ReservationEditPresenter(final WiseUiGinjector injector,
                                     final EventBus eventBus,
                                     final ReservationEditView view,
                                     final ReservationServiceAsync service,
                                     final ReservationManager reservationManager,
                                     final ReservationMessages messages) {
         ...
     }
     

Example 4: Long assignments

     final SecretReservationKey secretReservationKey
        = new SecretReservationKey(data.getUrnPrefix(), data.getSecretReservationKey());
		
Example 5: Long class signatures

	 public class SimpleSerialPortConnection extends AbstractConnection 
		 implements SerialPortConnection, SerialPortEventListener {
		 ...
	 }

[checkstyle]:http://checkstyle.sourceforge.net/
[maven-checkstyle-plugin]:http://maven.apache.org/plugins/maven-checkstyle-plugin/
