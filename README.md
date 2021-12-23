
import boto3
import json

def index_faces(photo, bucket):

    client=boto3.client('rekognition')

    response = client.detect_faces(Image={'S3Object':{'Bucket':bucket,'Name':photo}},Attributes=['ALL'])

    
    numfaces = len(response['FaceDetails'])
    if numfaces ==1:
            print('Detected faces for ' + photo)
        
            for faceDetail in response['FaceDetails']:
                print('The detected face is ' + str(faceDetail['AgeRange']['High']) + ' years old')



		# Access predictions for individual face details and print them
                print("Gender: " + str(faceDetail['Gender']))
                print("Emotions: " + str(faceDetail['Emotions'][0]))
    else:
        print('Error! 한 사람의 사진만 넣어주세요.')

    
    
    
    return len(response['FaceDetails'])
       
       

   
def main():
    photo="photo7.png"
    bucket="hyeonsudataupload"
    face_count=index_faces(photo, bucket)
    if face_count==1:
        print("Faces detected: " + str(face_count))


if __name__ == "__main__":
    main()
