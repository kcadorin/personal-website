# Custom Domain Setup Guide for kaleby.com.br

This guide explains how to configure your custom domain `kaleby.com.br` to work with your GitHub Pages site.

## ✅ Changes Already Made

1. ✓ Updated `baseURL` in `personal/hugo.toml` to `https://kaleby.com.br/`
2. ✓ Created `personal/static/CNAME` file with your domain
3. ✓ Updated OpenGraph URL in `personal/data/en/site.yaml`

## 🔧 DNS Configuration Steps

You need to configure DNS records with your domain registrar (Registro.br or your DNS provider). You have two options:

### Option 1: Apex Domain (Recommended)

If you want to use `kaleby.com.br` (without www):

#### Add A Records:
Point your apex domain to GitHub's IP addresses by creating **4 A records**:

```
Type: A
Name: @ (or leave blank for apex domain)
Value: 185.199.108.153

Type: A
Name: @ (or leave blank for apex domain)
Value: 185.199.109.153

Type: A
Name: @ (or leave blank for apex domain)
Value: 185.199.110.153

Type: A
Name: @ (or leave blank for apex domain)
Value: 185.199.111.153
```

#### Add AAAA Records (IPv6 - Optional but Recommended):
```
Type: AAAA
Name: @ (or leave blank)
Value: 2606:50c0:8000::153

Type: AAAA
Name: @ (or leave blank)
Value: 2606:50c0:8001::153

Type: AAAA
Name: @ (or leave blank)
Value: 2606:50c0:8002::153

Type: AAAA
Name: @ (or leave blank)
Value: 2606:50c0:8003::153
```

### Option 2: Using www Subdomain

If you want to use `www.kaleby.com.br`:

#### Add CNAME Record:
```
Type: CNAME
Name: www
Value: kaleby.github.io
```

### Option 3: Both (Apex + www)

To support both `kaleby.com.br` and `www.kaleby.com.br`:

1. Add all the **A records** from Option 1 for the apex domain
2. Add the **CNAME record** from Option 2 for www subdomain

## 🌐 Configure GitHub Pages

After updating your DNS records:

1. Go to your GitHub repository: https://github.com/kaleby/personal-website
2. Navigate to **Settings** → **Pages**
3. Under "Custom domain", enter: `kaleby.com.br`
4. Click **Save**
5. Wait for DNS check to complete (can take up to 24-48 hours)
6. Once DNS is verified, check **Enforce HTTPS** (recommended)

## 📝 DNS Propagation

- DNS changes can take anywhere from a few minutes to 48 hours to propagate worldwide
- You can check DNS propagation status at: https://dnschecker.org/
- Enter your domain `kaleby.com.br` to see if DNS records are visible globally

## 🔍 Verify Your Setup

### Check DNS Records (Terminal):
```bash
# Check A records
dig kaleby.com.br +short

# Check CNAME for www
dig www.kaleby.com.br +short

# Check AAAA records (IPv6)
dig kaleby.com.br AAAA +short
```

### Expected Results:
- A records should return GitHub's IPs: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
- CNAME should return: `kaleby.github.io`

## 🚀 Deployment Steps

After DNS is configured:

```bash
# Commit the changes
git add personal/hugo.toml personal/static/CNAME personal/data/en/site.yaml
git commit -m "Configure custom domain kaleby.com.br"
git push origin main
```

The GitHub Actions workflow will automatically deploy your site with the custom domain.

## 🔒 HTTPS/SSL Certificate

- GitHub Pages automatically provides free SSL certificates via Let's Encrypt
- After DNS verification, enable "Enforce HTTPS" in your repository settings
- It may take a few hours for the certificate to be issued
- Once enabled, your site will be accessible at `https://kaleby.com.br`

## 📋 Typical DNS Configuration Interface (Registro.br)

For Registro.br, the interface usually looks like this:

1. Log in to your Registro.br account
2. Go to "DNS" or "Gerenciar DNS"
3. Select your domain `kaleby.com.br`
4. Add new records:

```
Tipo    Nome    Valor                   TTL
A       @       185.199.108.153        3600
A       @       185.199.109.153        3600
A       @       185.199.110.153        3600
A       @       185.199.111.153        3600
AAAA    @       2606:50c0:8000::153    3600
AAAA    @       2606:50c0:8001::153    3600
AAAA    @       2606:50c0:8002::153    3600
AAAA    @       2606:50c0:8003::153    3600
CNAME   www     kaleby.github.io       3600
```

## ⚠️ Important Notes

1. **Remove conflicting records**: If you have existing A, AAAA, or CNAME records for `@` or `www`, you'll need to remove them first
2. **TTL (Time To Live)**: Set to 3600 seconds (1 hour) or use your provider's default
3. **Trailing dots**: Some DNS providers require a trailing dot (e.g., `kaleby.github.io.`) - check your provider's documentation
4. **CAA Records**: Optional, but you can add CAA records to authorize Let's Encrypt:
   ```
   Type: CAA
   Name: @
   Value: 0 issue "letsencrypt.org"
   ```

## 🆘 Troubleshooting

### Site Not Loading
- Wait 24-48 hours for full DNS propagation
- Check DNS records using `dig` or online tools
- Verify CNAME file is present in your repository

### HTTPS Not Available
- Ensure DNS is fully propagated
- Wait a few hours after DNS verification
- Uncheck and recheck "Enforce HTTPS" in GitHub settings

### Certificate Errors
- Clear browser cache
- Wait for Let's Encrypt to issue certificate (can take up to 24 hours)
- Verify DNS is pointing correctly

## 📚 Additional Resources

- [GitHub Pages Custom Domain Documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [Registro.br DNS Configuration](https://registro.br/tecnologia/ferramentas/dnsmaster/)
- [DNS Checker Tool](https://dnschecker.org/)
- [Let's Encrypt Status](https://letsencrypt.status.io/)

## 📧 Need Help?

If you encounter issues:
1. Check the GitHub Pages status: https://www.githubstatus.com/
2. Review GitHub Pages documentation
3. Contact your DNS provider support
4. Check the GitHub Community forums

---

**Last Updated**: October 1, 2025

