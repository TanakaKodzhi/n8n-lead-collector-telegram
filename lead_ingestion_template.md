{
  "name": "Принятие лидов из форм",
  "nodes": [
    {
      "parameters": {
        "content": "### 📌 Инструкция по настройке\n1. **Webhook**: скопируйте production-URL и вставьте в настройки отправки вебхуков вашей формы.\n2. **Edit Fields**: замените ключи `question_2bJMKb`, `question_x0PeJ9`, `question_ZGzp2v` на ключи полей вашей конкретной формы.\n3. **Send a text message**: укажите свои учетные данные Telegram и замените `YOUR_TELEGRAM_CHAT_ID` на ID вашего чата или группы.",
        "height": 170,
        "width": 420,
        "color": 6
      },
      "type": "n8n-nodes-base.stickyNote",
      "typeVersion": 1,
      "position": [
        60,
        -210
      ],
      "id": "18f921a4-9842-4fce-bc2a-89a19d7c6742",
      "name": "Sticky Note"
    },
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "webhook-leads",
        "options": {}
      },
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2.2,
      "position": [
        0,
        0
      ],
      "id": "a3930720-2f4c-4158-be5e-d054cf472477",
      "name": "Webhook"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "270ff1f8-c5b3-427f-bf69-60c9caa0b2cc",
              "name": "Имя",
              "value": "={{ $json.body.data.fields.find(f => f.key === 'question_2bJMKb')?.value }}",
              "type": "string"
            },
            {
              "id": "8bedf5bc-1798-4234-bc56-ce5df93eadfa",
              "name": "Номер Телефона",
              "value": "={{ $json.body.data.fields.find(f => f.key === 'question_x0PeJ9')?.value }}",
              "type": "string"
            },
            {
              "id": "075549b4-9fd8-4e78-86e7-79f408fa5334",
              "name": "почта",
              "value": "={{ $json.body.data.fields.find(f => f.key === 'question_ZGzp2v')?.value }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.5,
      "position": [
        224,
        0
      ],
      "id": "743cc3a1-eac6-4910-a43a-ae29fc828f84",
      "name": "Edit Fields"
    },
    {
      "parameters": {
        "chatId": "YOUR_TELEGRAM_CHAT_ID",
        "text": "=<b>🔥Новая заявка на консультацию</b>\n<b>имя:</b> {{ $json['Имя'] }}\n<b>номер телефона:</b> <i>{{ $json['Номер Телефона'] }}</i>\n<b>почта:</b> <code>{{ $json['почта'] }}</code>",
        "additionalFields": {
          "appendAttribution": false,
          "parse_mode": "HTML"
        }
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        448,
        0
      ],
      "id": "52820be2-d1e5-48e4-9a13-3d5b0cdbaaba",
      "name": "Send a text message"
    }
  ],
  "pinData": {},
  "connections": {
    "Webhook": {
      "main": [
        [
          {
            "node": "Edit Fields",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Edit Fields": {
      "main": [
        [
          {
            "node": "Send a text message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1",
    "binaryMode": "separate",
    "timezone": "UTC"
  },
  "meta": {
    "templateCredsSetupCompleted": false
  },
  "tags": []
}