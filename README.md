from ibm_watson import VisualRecognitionV3
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

# Replace with your API key and endpoint
apikey = 'your_api_key'
url = 'your_service_endpoint'

# Initialize Visual Recognition service
authenticator = IAMAuthenticator(apikey)
visual_recognition = VisualRecognitionV3(
    version='2018-03-19',
    authenticator=authenticator
)

# Set the service endpoint
visual_recognition.set_service_url(url)

# Example image file path
image_path = 'path_to_your_image.jpg'

# Perform image recognition
with open(image_path, 'rb') as images_file:
    classes = visual_recognition.classify(
        images_file=images_file,
        threshold='0.6',
        classifier_ids='default'
    ).get_result()

# Print results
print(json.dumps(classes, indent=2))
