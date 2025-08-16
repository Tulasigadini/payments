
api end points
===============
POST http://localhost:8000/webhook/payments 
haders=>X-Razorpay-Signature :1e55af4e30f3a59e19c669a86ec9df614a277bdf51b14291630f7fd7134d4b53
json body=> {"event":"payment.authorized","payload":{"payment":{"entity":{"id":"pay_0114","status":"authorized","amount":5000,"currency":"INR"}}},"created_at":1751889865,"id":"evt_auth_0114"}

generate this Razorpay-Signature by running /webhook_system\payments> python .\signature.py
response
==========
{
    "status": "success",
    "event_id": "evt_auth_0114",
    "payment_id": "pay_0114",
    "received_at": "2025-08-16T15:22:53.070591Z"
}
2)get http://localhost:8000/payments/pay_014/events or http://localhost:8000/payments/{payment_id}/events

response
------------
[
    {
        "event_type": "payment.authorized",
        "received_at": "2025-08-16T08:54:41.441552+00:00Z"
    }
]
