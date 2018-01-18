# Ejercicios de Arquitecturas software para la nube
======================================================================

# Ejercicio 1º
## Buscar una aplicación de ejemplo, preferiblemente propia, y deducir qué patrón es el que usa. ¿Qué habría que hacer para evolucionar a un patrón tipo microservicios?

Como aplicación de ejemplo se utilizará la realizada para el TFG. "Erasmus Management System" es una aplicación que lleva a cabo todo el proceso documental ligado al Erasmus, desde la preinscripción hasta el regreso del alumno, implicando a todos los actores implicados (coordinadores, profesores, alumnos, secretarios, personal de administración, etc). En esta aplicación se puede observar una arquitectura en capas distinguiendo las capas de presentación, aplicación, lógica de negocio y acceso a datos.

Para conseguir una migración al patrón de tipo microservicios, se podrían dividir los servicios para realizarlos a través de máquinas virtuales o contenedores en la nube. Facilitando su ejecución y permitiendo su despliegue independiente.

# Ejercicio 2º
## En la aplicación que se ha usado como ejemplo en el ejercicio anterior, ¿podría usar diferentes lenguajes? ¿Qué almacenes de datos serían los más convenientes?

La realización de la aplicación mencionada se programó a través del framework CakePhp.

Por supuesto podrían utilizarse diversos lenguajes como python o javascript, o incluso llegar a realizar algunos de sus servicios con pearl.

En cuanto al almacenamiento de datos, se optó por una base de datos relacional MySQL. Sin embargo su realización a través de MongoDB hubiese sido más acertada.
