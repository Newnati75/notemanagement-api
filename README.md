#%RAML 1.0
title: Notes Management API
version: v1
baseUri: http://localhost:8081/api

mediaType: application/json

types:
  Note:
    type: object
    properties:
      id: integer
      title: string
      content: string
      createdAt?: datetime
      updatedAt?: datetime

  NoteInput:
    type: object
    properties:
      title: string
      content: string
    required: [title, content]

  ErrorResponse:
    type: object
    properties:
      message: string

/notes:
  get:
    description: Get all notes
    responses:
      200:
        body:
          type: Note[]

  post:
    description: Create a new note
    body:
      application/json:
        type: NoteInput
    responses:
      201:
        body:
          type: Note
      400:
        body:
          type: ErrorResponse

/notes/{id}:
  uriParameters:
    id:
      type: integer
      required: true

  get:
    description: Get a note by ID
    responses:
      200:
        body:
          type: Note
      404:
        body:
          type: ErrorResponse

  put:
    description: Update a note by ID
    body:
      application/json:
        type: NoteInput
    responses:
      200:
        body:
          type: Note
      404:
        body:
          type: ErrorResponse

  delete:
    description: Delete a note by ID
    responses:
      204:
        description: Note deleted successfully
      404:
        body:
          type: ErrorResponse
