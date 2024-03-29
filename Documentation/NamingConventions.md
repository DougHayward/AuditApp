<h1>"Audit App / SolutionMVC / SolutionORM" Naming conventions and other documentation.</h1>

<p>
    This document is intended to outline the various naming conventions used in 
    the listed projects and also provide a basic understanding of how things work.
    Some aspects of the framework code will not function if these conventions are 
    not adhered to, whereas other conventions are simply for continuity and readability.
    Where possible it is encouraged you stick to the conventions in order to make 
    the code more future proofed, if all in house developers stick to these rules 
    when new people join us they won't be flying so blind.
</p>

<p>
    I'll keep it as short and as simple as possible because no one likes reading 
    endless lines of shit.
</p>

<h3>Contents</h3>
<ul>
    <li>Database Tables</li>
    <li>Controllers</li>
    <li>Actions</li>
</ul>


<h2>Database Tables</h2>

<h3>Table Names</h3>

<h4>Standard Tables</h4>
<p>Normal tables should be camel cased and pluralised (Not required).</p>
<code>Example: UserActivities, Clients,  ApiKeys</code>

<h4>Join Tables</h4>
<p>Join tables should be the singular name of each joining table, camel cased if required. Seperated by an underscore (Not required).</p>
<code>Example (Many users belong to many groups"): Users -> 1m -> User_Group <- m1 <- Groups </code>



<h2>Controllers</h2>
<h3>Controllers (PHP)</h3>
<i>namespace SolutionMvc\Controller;</i>
<p>Controllers should be camel cased and postfixed with 'Controller'. Class names should be the same as the file name (Required for controllers called by routes)</p>
<code>Example: UserController.php (class UserController{}),
               AuditController.php (class AuditController{}),
               SecurityController.php (class SecurityController{})
</code>

<h2>Actions</h2>
<h3>Actions (PHP)</h3>
<i>namespace SolutionMvc\Controller;</i>
<p>Actions should only ever produce an output string. JSON/String/Int <STRONG>NEVER</STRONG> html or view content. 
The front end should handle creating a view out of the output data. 
This helps keep seperation of concerns and faciliates with unit testing.</p>
<p>Actions are the base functions within controllers. They should be post fixed with Action, be camel cased with lowercase first latter.(Required for actions called by routes)</p>
<code>For example you want to get User 10. The route would resemble https://localhost/User/getUser/10 this would call the getUserAction($id) from the UserController{} passing the '$id = 10' to the function.</code>
<code>For example you want to get User username: dhayward, client: 000. The route would resemble https://localhost/User/getUser/dhayward/000 this would call the getUserAction($username, $client) from the UserController{} passing the '$username = "dhayward"', $client = "000"' to the function.</code>

<h3>Example Controller with Actions</h3>

<code>

    namespace SolutionMvc\Controller;

    class AuditController {

        public function indexAction() {
            return print '
                [
                    {
                    "id":"1",
                    "name":"Some audit",
                    "created_at":"11/11/16"
                    },
                    {
                    "id":"2",
                    "name":"Some audit 2",
                    "created_at":"09/01/16"
                    }
                ]            
                ';
        }
        public function getAction($id = "1") {
            if ($id == "1") {
                $response = '                
                    {
                    "name": "Some audit",
                    "description": "A description"
                    };
            }
        }
    }


</code>

<h3>Models (PHP)</h3>
<p>Model classes should be simply the name of the table with no spaces and singular.</p>
<code>Example: User.php (class User extends BaseModel{})</code>
<code>Example: Answer.php (class Answer extends BaseModel{})</code>

