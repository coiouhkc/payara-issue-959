# payara-issue-959
Sample project to illustrate the issue #959 in Payara

Steps to reproduce:
* mvn clean install
* export MAVEN_REPO=<path_to_current_maven_repo>
* mvn test

Sample output:
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 18 at position9
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 0 at position10
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 0 at position11
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 0 at position12
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 57 at position13
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 18 at position15
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 0 at position16
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 105 at position18
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 110 at position19
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 101 at position20
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 78 at position21
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 117 at position22
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 109 at position23
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 98 at position24
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 101 at position25
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 114 at position26
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 84 at position27
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 97 at position28
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 98 at position29
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 108 at position30
Jul 29, 2016 11:45:45 AM com.sun.enterprise.deployment.annotation.introspection.ConstantPoolInfo containsAnnotation
SCHWERWIEGEND: Unknow type constant pool 101 at position31

Problem:
ALthough not directly reproducible (no BufferUnderflowException occurs), it's obvious, that ConstantPoolInfo class is reading weirdest numbers after not being able to parse the initial '18' - CONSTANT_InvokeDynamic, see http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-4.html#jvms-4.4 .
