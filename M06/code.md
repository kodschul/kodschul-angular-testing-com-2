
# Angular End-to-End Testing mit Protractor

## Themen

1. Schreiben eines End-to-End-Tests mit Seitenobjekten
2. Erstellen eines Seitenobjekts für eine Komponente
3. Testen komplexer Interaktionen mit Protractor

## 1. Schreiben eines End-to-End-Tests mit Seitenobjekten

### Live Coding Beispiel

In der Datei `app.po.ts`:

```typescript
import { browser, by, element } from 'protractor';

export class AppPage {
  navigateTo(): Promise<unknown> {
    return browser.get(browser.baseUrl) as Promise<unknown>;
  }

  getTitleText(): Promise<string> {
    return element(by.css('app-root .content span')).getText() as Promise<string>;
  }
}
```

In der Datei `app.e2e-spec.ts`:

```typescript
import { AppPage } from './app.po';

describe('workspace-project App', () => {
  let page: AppPage;

  beforeEach(() => {
    page = new AppPage();
  });

  it('should display the title message', async () => {
    await page.navigateTo();
    expect(await page.getTitleText()).toEqual('app works!');
  });
});
```

## 2. Erstellen eines Seitenobjekts für eine Komponente

### Live Coding Beispiel

In der Datei `login.po.ts`:

```typescript
import { element, by, browser } from 'protractor';

export class LoginPage {
  navigateTo(): Promise<unknown> {
    return browser.get('/login') as Promise<unknown>;
  }

  setUsername(username: string): void {
    element(by.css('input[name="username"]')).sendKeys(username);
  }

  setPassword(password: string): void {
    element(by.css('input[name="password"]')).sendKeys(password);
  }

  clickLoginButton(): void {
    element(by.css('button[type="submit"]')).click();
  }
}
```

**Test:**

```typescript
import { LoginPage } from './login.po';

describe('Login Page', () => {
  let page: LoginPage;

  beforeEach(() => {
    page = new LoginPage();
  });

  it('should login with correct credentials', async () => {
    await page.navigateTo();
    page.setUsername('testuser');
    page.setPassword('password123');
    page.clickLoginButton();
    // Überprüfung des Erfolgs oder der Navigation
  });
});
```

## 3. Testen komplexer Interaktionen mit Protractor

### Live Coding Beispiel

In der Datei `dashboard.po.ts`:

```typescript
import { element, by, browser } from 'protractor';

export class DashboardPage {
  navigateTo(): Promise<unknown> {
    return browser.get('/dashboard') as Promise<unknown>;
  }

  clickMenuButton(): void {
    element(by.css('.menu-button')).click();
  }

  selectMenuItem(itemName: string): void {
    element(by.cssContainingText('.menu-item', itemName)).click();
  }
}
```

**Test:**

```typescript
import { DashboardPage } from './dashboard.po';

describe('Dashboard Page', () => {
  let page: DashboardPage;

  beforeEach(() => {
    page = new DashboardPage();
  });

  it('should navigate through the menu', async () => {
    await page.navigateTo();
    page.clickMenuButton();
    page.selectMenuItem('Settings');
    // Überprüfung der Anzeige der Einstellungen-Seite
  });
});
```