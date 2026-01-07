#include <Stdio.h>
#include <string.h>
#include <stdlib.h>

typedef struct {
  int id;
  char name[50];
  char disease[50];
  int days_admitted;
} Patient;
Patient* creatingArray(int *size);
void admitPatient(Patient *hospital ,int *size, int *numberPatient);
void discharge(Patient *hospital, int *numberPatient);
void searching(Patient *hospital, int *numberPatient);
void printing(Patient *hospital, int *numberPatient);

int main() {
  int size = 100;
  int numberPatient = 0;
  Patient *hospital = creatingArray(&size);
  int user_choice;
  printf("Please Enter a number between 1 to 5 : ");
  scanf("%d", &user_choice);
  while(getchar() != '\n');
  while (user_choice != 5) {
    switch(user_choice) {
      case 1:
      admitPatient(hospital , &size, &numberPatient);
      break;
      case 2:
        discharge(hospital, &numberPatient);
      break;
      case 3:
        searching(hospital,&numberPatient);
      break;
      case 4:
        printing(hospital, &numberPatient);
      break;
      case 5:
        printf("Thank you for our services\n");
      break;
      default:
      printf("Please Enter a number between 1 to 5\n");
    }
    printf("Please Enter a number between 1 to 5 : ");
    scanf("%d", &user_choice);
    while(getchar() != '\n');
  }

  return 0;
}

Patient* creatingArray(int *size) {
  Patient *hospital = malloc((*size) * (sizeof(Patient)));
  return hospital;
}

void admitPatient(Patient *hospital ,int *size, int *numberPatient) {
  int addPatient = 0;
  printf("How many patient do you wanna add : ");
  scanf("%d",&addPatient);
  while(getchar() != '\n');
  if( (addPatient + (*numberPatient)) <= *size) {
    for(int i =  (*numberPatient); i < addPatient + (*numberPatient); i++) {
      printf("please Enter the id of the %dth patient : ", i+1);
      scanf("%d",&hospital[i].id);
      while(getchar() != '\n');
      
      printf("Please enter the name of the %dth patient : ", i+1 );
      fgets(hospital[i].name, sizeof(hospital[i].name),stdin);
      hospital[i].name[strcspn(hospital[i].name,"\n")]= '\0';
      
      printf("Please enter the disease of the %dth patient :", i+1);
      fgets(hospital[i].disease, sizeof(hospital[i].disease),stdin);
      hospital[i].disease[strcspn(hospital[i].disease, "\n")] = '\0';
      
      printf("Please enter the number of days which the %dth pathient admitted ", i+1);
      scanf("%d",&hospital[i].days_admitted);
      while(getchar() != '\n');
    }
    *numberPatient = (*numberPatient)  + addPatient;
  }
  else {
    printf("We are sorry due to there is no any bed in hospital\n");
  }
}

void discharge(Patient *hospital, int *numberPatient) {
  int idPatient;
  int found = 0;
  printf("Enter the ID of the patient who you want to discharge");
  scanf("%d",&idPatient);
  while(getchar() != '\n');

  for(int i = 0; i < *numberPatient; i++) {
    if(hospital[i].id == idPatient) {
      float bill = hospital[i].days_admitted * 150.00;
      printf("The final bill is : %.2f$ \n",bill);
      for(int j = i; j < *numberPatient-1; j++ ){
        hospital[j] = hospital[j+1];
        found = 1;
        
      }  
      (*numberPatient)--;
      break;
    }
  }
  if(found ==  0) {
    printf("there is no patient found with this match\n");
  }
}

void searching(Patient *hospital, int *numberPatient) {
  char namePatient[50];
  int found = 0;
  printf("Please Enter the name of the patient thyou  : ");
  fgets(namePatient, sizeof(namePatient), stdin);
  namePatient[strcspn(namePatient,"\n")] = '\0';
  for(int i = 0; i < *numberPatient; i++) {
    if(strcmp(hospital[i].name, namePatient) == 0){
      printf("%d- ID: %d Name: %s Disease: %s Day of Admitted : %d\n", i+1,hospital[i].id, hospital[i].name ,hospital[i].disease, hospital[i].days_admitted);
      found = 1;
    }
  }
  if(found == 0) {
    printf("There is no patient with the information\n");
  }
}

void printing(Patient *hospital, int *numberPatient) {
  for(int i= 0; i < *numberPatient; i++) {
    printf("%d- ID: %d Name: %s Disease: %s Day of Admitted : %d\n", i+1,hospital[i].id, hospital[i].name ,hospital[i].disease, hospital[i].days_admitted);
  }
}










