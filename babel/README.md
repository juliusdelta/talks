## Resources

[Javascript compatibility chart](https://kangax.github.io/compat-table/es2016plus/)

[Babel Docs](https://babeljs.io/docs/en/)

[AST Explorer](https://astexplorer.net/#/KJ8AjD6maa)

[@babel/plugin-proposal-optional-chaining](https://github.com/babel/babel/tree/master/packages/babel-plugin-proposal-optional-chaining)

## Outline

- Why?
    - We need to understand our tools. What we do is a craft, like iron working (analogy), so understanding our tools is vitally important.
    - With tools like create-react-app it's tough to know what it takes to get your code to execute on the client side.
    - You'll be able to customize your build process more and if done wisely you can maximize your efficiency and developer experience.
- What is Babel?
    - Babel is Google Translate for your javascript.
    - Not all JS is enabled for all browsers
        - example: Optional Chaining
- How does Babel work?
    - It parses your code using a parser called Babylon into an Abstract Syntax Tree
    - An Abstract Syntax Tree is simply a giant object describing your code and what to do with it
        - Example: Walk through @babel/plugin-proposal-optional-chaining
            - Example Code

                    // test code
                    function test() {
                      const obj = {
                        person: {
                          name: "JD",
                          friends: [
                            { name: "David" },
                            { name: "Ronak" },
                            { name: "Josh" }
                          ]
                        }
                      }
                      
                      return obj?.age;
                    }
                    
                    // babel code
                    export default function(babel) {
                      const { types: t } = babel;
                    
                      return {
                        name: "ast-transform", // not required
                        visitor: {
                          Identifier(path) {
                            if (true && path.container.type === "OptionalMemberExpression") {
                              console.log(path);
                            }
                          }
                        }
                      };
                    }

    - Performs pre-determined operations when the code is parsed to change it
        - Example

                // Before
                obj?.person?.age
                
                // After
                if (obj && obj.person && obj.person.age) { 
                  return obj.age;
                } else {
                  return null
                }

-