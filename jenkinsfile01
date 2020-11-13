node {
agent any
    parameters {
        string(name: 'GITURL', defaultValue: 'https://github.com/SilvanoGil/curso_integracion_continua.git', description: 'Url Git')
    }
	stage('Git') {
       sleep 3
	   git ${params.GITURL}
       echo "Finaliza etapa Git"
    }
    stage('Maven') {
                sleep 3
				bat 'mvn clean'
                echo "Finaliza etapa build"  
				input {
                message "Desea Continuar?"
                ok "Si"
                submitter "Isi"	
				}		
				sleep 5
				bat 'mvn pmd:pmd checkstyle:checkstyle package'
    }
     stage('Guarda') {
                sleep 3
				archiveArtifacts artifacts: 'webapp/target/*.war', followSymlinks: false
                echo "Finaliza etapa guardar"           
    }
    stage('Despliega a Tomcat') {
       sleep 3
       deploy adapters: [tomcat8(credentialsId: '87696c85-19d3-493e-8bbc-ef6d3a86423d', path: '', url: 'http://localhost:8081')], contextPath: null, war: '**/*.war'
	   echo "Finaliza Despliegue"
    }
}
