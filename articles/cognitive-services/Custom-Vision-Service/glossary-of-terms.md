---
title: Glossary of Terms for Custom Vision Service machine learning | Microsoft Docs
description: Glossary of Terms for Custom Vision Service.
services: cognitive-services
author: v-royhar
manager: juliakuz
ms.service: cognitive-services
ms.technology: custom vision service
ms.topic: article
ms.date: 05/08/2017
ms.author: v-royhar
ms.translationtype: Human Translation
ms.sourcegitcommit: 71fea4a41b2e3a60f2f610609a14372e678b7ec4
ms.openlocfilehash: d13590b5a2f8102789d524854b3a0ce4e57aba90
ms.contentlocale: ja-jp
ms.lasthandoff: 05/10/2017

---
# <a name="glossary"></a>Glossary

The following are some terms used in Custom Vision Service, and their meaning.

## <a name="classifier"></a>Classifier

A classifier is a model you build using Custom Vision Service, by using a few training images. Once you have finished training a new classifier, you receive an evaluation endpoint (HTTPS) you can add to your app. Each classifier you build is in its own project, and you can view all projects once you have signed in.

## <a name="domain"></a>Domain

When you create a project, you select a "domain" for that project. The domain optimizes a classifier for a specific type of object in your images. For example, if your scenario is to classify between images of apple pie versus images of carrot cake, then select the "Food" domain. If you are unsure of which domain to choose, then select "Generic" domain.

- **The Food domain.** Optimized for dishes you would see on a restaurant menu. It was not optimized for recognizing individual fruit or vegetables. If you want to classify photographs of individual fruits or vegetables, use the Generic domain for that purpose.
- **The Landmark domain.** Optimized for recognizable landmarks, both natural and artificial. This domain works best when the landmark is clearly visible in the photograph, even if the landmark is slightly obstructed by a group of people posing in front of it.
- **The Retail domain.** Optimized for classifying images in a shopping catalog or shopping website. If you want high precision when classifying dresses, pants, shirts, etc., then use the Retail domain.
- **The Adult domain.** Optimized to better define between adult content and non-adult content. For example, if you want to block images of people in bathing suits, this domain allows you to build a custom classifier to do that.

## <a name="training-image"></a>Training Image

To create a high precision classifier, Custom Vision Service needs several training images. A training image is a photograph of the image you want Custom Vision Service to classify. For example, to classify oranges, you would need to upload several images of oranges to Custom Vision Service to allow the service to create a classifier that can recognize oranges. We recommend at least 30 images per tag.

## <a name="iteration"></a>Iteration

Every time you Train or re-train your classifier, you create a new iteration of your model. We keep several past iterations to allow you to compare your progress over time. You can delete any iteration you no longer find useful. Remember that deleting an iteration is permanent, and you also delete any images or changes that were unique to that iteration. 

## <a name="workspace"></a>Workspace

Your workspace contains all your training images, and it reflects all changes from your most recent iteration such as removed or added images. When you Train your classifier, you create a new iteration of your classifier, by using the images present in your Workspace.

## <a name="tags"></a>Tags

Use tags to label the objects in your training images. If you are creating a classifier to identify dogs and ponies, you would put a "dog" tag on images that contain dogs, a "pony" tag on images that contain ponies, and both a "dog" and a "pony" tag on images that contain both a dog and a pony.

## <a name="evaluation"></a>Evaluation

Once you have trained your classifier, you can submit any image for evaluation by using the auto-generated https endpoint. Your classifier returns a set of predicted tags, in order of confidence.

## <a name="predictions"></a>Predictions

As your classifier accepts new images to classify, it stores the images for you. You can use these images to improve the precision of your classifier by correctly tagging the mis-predicted images. You can then use these new images to re-train your classifier.

## <a name="precision"></a>Precision

When you classify an image, how likely is your classifier to correctly classify the image? Out of all images used to train the classifier (dogs and ponies), what percent did the model get correct? 99 correct tags out of 100 images gives a Precision of 99%.

## <a name="recall"></a>Recall

Out of all images that should have been classified correctly, how many did your classifier identify correctly? A Recall of 100% would mean, if there were 38 dog images in the images used to train the classifier, 38 dogs were found by the classifier.

## <a name="settings"></a>Settings

There are two types of settings, Project-Level settings and User-Level settings.

- Project-Level settings: 
  
  Project-level settings apply to a project or classifier. They include:

   - Project-domain
   - Project Name
   - Project Description
   - Usage:
      - Number of training images
      - Number of tags created
      - Number of iterations created

- User-Level settings: 
   - Subscription Keys: one for Training, one for Evaluation/Prediction.
   - Usage:
      - Number of projects created
      - Number of Evaluation/Prediction API calls made.

