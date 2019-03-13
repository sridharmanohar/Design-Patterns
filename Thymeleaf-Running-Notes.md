
## th:object
1. Used in forms.
2. The value of this attribute refers to an object to which the form in question refers to and thereby have access to.
3. Most forms are bean-backed that is there is an object/pojo to which they map.
4. The value of this attribute, which is the name of the pojo/object, should always be init case, i.e., if the name of the object os PersonalDirectoty then the value of th:object should be personalDirectory, then spring will be able to automatically map the object wih the form.
5. And since objects in thymeleaf are considered as variables, you use a $ to access the object.
6. Ex: th:object="${personalDirectoty}"

## th:action
1. Used in forms.
2. To specify the endpoint where this form has to be submitted to.
3. Uses @ - which is a link expression in the attribute to specify the endpoint.
4. Ex: th:action="@{/}" - this submits the form to controller handling requests at "/" path.

## th:field
1. Used to map a input field in the html to a property/field in the object to which this form has access to.
2. Either uses * or $ to map to the field.
4. Ex: th:field="*{firstName}" or th:field="${personalDirectory.firstName}"
