ITM Build Tools
===============

ITM Build Tools shall help to ease and harmonize e.g. the coding style in our ITM projects.

Checkstyle
----------

We use [Checkstyle][checkstyle] to enforce certain coding style guidlines.

Usage
-----

In your POM:

    <project>
      <build>
    	[...]
    	<pluginManagement>
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
                           <configLocation>build-tools/src/main/resources/itm_checks.xml</configLocation>
    			           <enableRulesSummary>false</enableRulesSummary>
                       </configuration>
                   </plugin>
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
    </project>

Generate a report on the command line:

  $ mvn checkstyle:checkstyle site

This generates a checkstyle reportand a HTML page. "site" makes sure, that all css-Files, etc. are avaiable. The html page(s) is(are) located at ${module}/target/site/checkstyle.html. If you are only interested in the plain report, you can leave out the "site" target.

More info can be found at: [checkstyle] und [maven-checkstyle-plugin].


[checkstyle]:http://checkstyle.sourceforge.net/
[maven-checkstyle-plugin]:http://maven.apache.org/plugins/maven-checkstyle-plugin/