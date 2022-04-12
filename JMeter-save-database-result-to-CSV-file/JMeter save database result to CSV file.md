## JMeter save database result to CSV file.

Add BenShell PostProcessor for JDBC Request.
`result` is the Result variable name of JDBC request.

### BeanShell PostProcessor
```bash
import org.apache.jmeter.services.FileServer;

String paramsCounts = String.valueOf( vars.getObject("result").size() );
props.put("counts", paramsCounts); // Global property variable to share data to another thread.

File file = new File("/Users/mahmud/files/file.csv"); // CSV file path
FileWriter fstream = new FileWriter(file);

BufferedWriter out = new BufferedWriter(fstream);
private static final String newLine = System.getProperty("line.separator");
for (int i = 0 ; i < vars.getObject("result").size() ; i ++) {

	String param = vars.getObject("result").get(i).get("parameter_id").toString(); // parameter_id is the column name
	out.write(param +  newLine );

}
out.close();
fstream.close();
```

### Scenario 101
Run another Thread as Database result size.
```
${__P(counts)}
```
For Number of Threads(users): `${__P(counts)}`
Now This thread will run as the number of row found from database query.
